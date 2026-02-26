---
name: ascendc
description: Guides the agent to develop AscendC transformer GMM-style custom ops (such as grouped_matmul_finalize_routing) and their CANN aclnn examples by following existing patterns under ops-transformer/gmm and attention/softmax_ops/examples. Use when adding or modifying these ops, their kernels, tiling/infershape logic, or CANN API examples.
---

# AscendC GMM / 路由类算子开发

本技能指导 agent 按现有模式开发/修改 AscendC transformer GMM 类算子（如 `grouped_matmul_finalize_routing`）以及对应的 CANN `aclnn_*` 示例代码。

## 使用时机

在以下场景应用本技能：

- 需要新增或修改 GMM / 路由类 AscendC 算子（例如 Mixture-of-Experts 或 Grouped Matmul 相关）
- 需要为已有 AscendC 算子补充 `op_host` 定义、tiling / infershape 或 `op_kernel` 实现
- 需要编写类似 `attention/softmax_ops/examples/test_aclnn_softmax_ops.cpp` 的 CANN `aclnn_*` 示例
- 需要对这些算子进行对齐、重构或 bug 修复，同时保持与现有算子风格一致

---

## 总体工作流

当用户要求开发/修改此类算子时，按下面步骤执行（顺序很重要）：

1. **定位参考算子/示例**
   - 在 `ops-transformer/gmm/`、`ops-transformer/attention/` 下查找：
     - `*_def.cpp`（算子定义）
     - `*_tiling*.h/.cpp`（tiling、调度逻辑）
     - `op_kernel/*.h`（AscendC kernel 实现）
   - 在 `attention/softmax_ops/examples/` 或其他 `examples/` 目录下查找对应的 CANN `aclnn_*` 示例，例如：
     - `test_aclnn_softmax_ops.cpp`

2. **在 op_host 中定义 Graph 算子接口**
3. **在 op_kernel 中实现 AscendC kernel（含量化/路由逻辑）**
4. **补齐/复用 tiling、infershape 与注册逻辑（如果相关文件存在）**
5. **编写或更新 CANN API 示例与单测**

后续各节会具体说明每一步要做什么、关注哪些细节。

---

## 步骤一：复用现有模式

### 必读参考

- Graph 定义参考：
  - `ops-transformer/gmm/.../op_host/grouped_matmul_finalize_routing_def.cpp`
- AscendC kernel 实现参考：
  - `ops-transformer/gmm/.../op_kernel/grouped_matmul_finalize_routing.h`
- CANN API 示例参考：
  - `ops-transformer/attention/softmax_ops/examples/test_aclnn_softmax_ops.cpp`

### 行为规范

- **永远从现有同类算子拷贝骨架，再做最小必要修改**
- 保持：
  - 命名风格（文件名、类名、命名空间）
  - 宏使用方式（`ASCEND_IS_AIC`、`ASCEND_IS_AIV` 等）
  - 队列、UB buffer 管理模式（`TQue`、`TPipe`）
  - AICore 配置与不同芯片支持方式（例如 `ascend910b` / `ascend910_95`）

---

## 步骤二：在 op_host 中定义算子接口

参考 `grouped_matmul_finalize_routing_def.cpp` 的写法：

### 关键模式

- 继承 `OpDef`，在 `namespace ops` 内定义类，并使用 `OP_ADD` 注册：
  - 输入：
    - 使用 `Input("name")` + `.ParamType(REQUIRED/OPTIONAL)`
    - 明确 `.DataType({ ... })`、`.Format({ ... })` 与 `.UnknownShapeFormat({ ... })`
    - 支持多场景/多类型时，用向量形式列出所有组合
  - 输出：
    - 使用 `Output("y")`，同样配置 DataType / Format
  - 属性：
    - 用 `.Attr("attr_name").AttrType(OPTIONAL/REQUIRED).Int/Float/Bool/ListInt(...)` 设置默认值
  - AICore 配置：
    - 构造 `OpAICoreConfig`，设置：
      - `DynamicCompileStaticFlag(true)`
      - `DynamicFormatFlag(true)`
      - `DynamicRankSupportFlag(true)`
      - `DynamicShapeSupportFlag(true)`
      - `NeedCheckSupportFlag(false)`（如参考算子这么写）
      - 必要的 `ExtendCfgInfo(...)`，例如 `"softsync.flag"`, `"prebuildPattern.value"`, `"coreType.value"`, `"aclnnSupport.value"`
    - 按芯片型号调用 `this->AICore().AddConfig("ascend910b", config);` 等
  - 末尾用 `OP_ADD(YourOpClassName);` 完成注册

### Agent 要点

- 为新算子时：
  - **从参考算子完整复制类声明和构造函数体**，然后只改：
    - 类名 / 文件名
    - 输入输出名称与数量
    - 支持的 `DataType` / `Format`
    - 特有属性与默认值
  - 如无特殊理由，不要随意改动参考算子已有的 AICore flag 与 `ExtendCfgInfo` 结构
- 如果需要支持 `aclnn`：
  - 仿照参考算子中的 `"aclnnSupport.value", "support_aclnn"` 配置

---

## 步骤三：在 op_kernel 中实现 AscendC kernel

参考 `grouped_matmul_finalize_routing.h`，典型特征：

- 使用 `namespace GroupedMatmulFinalizeRouting`
- 引入：
  - `kernel_operator.h`
  - `lib/matmul_intf.h`
  - 自己的工具头文件（如 `grouped_matmul_finalize_routing_utils.h`）
- 定义类型别名：
  - `using aT = MatmulType<...>;`
  - `using bT = MatmulType<...>;`
  - `using BiasT = ...;`
  - `using cT = ...;`
  - `using MT = matmul::MatmulImpl<aT, bT, cT, BiasT, CFG_MDL>;`
- 使用模板参数控制不同场景：
  - 例如 `Param` 结构体模板携带：
    - 是否 `combine`
    - `ROW_INDEX_DTYPE`
    - `TILING_TYPE`
    - `SCALE_TYPE`
    - 是否有 `groupListType` / `sharedInputIsNone` / `transpose` 等

### 典型结构（参考即可，勿死记）

- 工具函数：
  - 如 `DataCopyPad2D`，有 GM↔UB 两个重载，带 `DataCopy2DDimParams`
- 主要类：
  - `template <class P> class QuantGroupMatmul`
    - `Init(...)`：根据 `initParams` 和 `tiling` 设置：
      - 多个 `GlobalTensor<...>`：
        - 输入、权重、bias、workspace、scale、per-token scale、group list、logits、residual、token ranks、输出等
      - 读取 `tiling` 中控制 flag（如 `deterministicFlag`, `hasPertokenScale`, `hasBias`）
      - 初始化队列和 UB buffer（`InitUbBuffer`）
    - `Process()`：整体执行流程，包含：
      - AIV / AIC 的分工、`PreProcess`（初始化输出、shared input 处理）
      - 循环 group、按 tiling 分块，依次：
        - `MMCompute(...)`：设置 matmul 形状、GM offset、workspace offset，调用 `mm.Iterate()` 做矩阵乘
        - `VectorSync(...)` + `FRDeterministic(...)`：处理 deterministic 模式
        - `VectorCompute(...)`：处理反量化、per-token scale、bias、atomic 写回
    - 若新算子逻辑相近，**尽量复用这一整套结构，只做必要变更**

### Agent 要点

- 为新算子/变体时：
  - 先确认：
    - 是否仍基于 `MatmulImpl`，以及需要哪些 GM tensor
    - tiling 结构里有哪些字段（例如 `matmulTiling.baseM/baseN/k`、`groupNum` 等）
  - 修改点仅限：
    - 新增/删减 GM 输入（例如多了一个 scale/bias/logits）
    - 调整 `ComputeDequantAndActivate` / `PerTokenScaleBrcb` 等中使用的张量组合
    - 修改 `InitOutputWithZeros`、`PreProcess` 中与业务强相关的初始化逻辑
  - 保持：
    - 队列/UB 分配、`PipeBarrier`、`DataCopyPad`、`SetAtomicAdd` 这些模式不变，除非有明确 bug 或需求

---

## 步骤四：tiling / infershape / 其他 host 逻辑

虽然本技能示例未展开全部文件，但 agent 在代码库中应遵循以下模式：

1. 在 `op_host/` 下查找：
   - `*_tiling*.h/.cpp`
   - `*_infershape.cpp`
   - 其他 `${op_name}_*.cpp` 文件
2. 分析参考算子中的：
   - tiling 入参（batch、M/N/K、group 数、是否 deterministic 等）
   - 如何把 Graph 级别 shape/attr 转为 kernel 所需的 `tiling` 结构
3. 为新算子时：
   - 若语义接近，优先复制参考 tiling/infershape 代码后改名、改字段
   - 确保：
     - Graph 中的 attr / shape 能正确映射到 kernel 中访问的 `tiling->...` 字段
     - deterministic 开关、workspace size、coreNum / parallNum 等计算逻辑保持一致风格

---

## 步骤五：CANN aclnn 示例（examples）

参考 `test_aclnn_softmax_ops.cpp`，模式如下：

1. **通用工具函数**
   - `GetShapeSize`：计算形状乘积
   - `PrintOutResult<T>`：将 device 结果拷回 host 并打印
   - `Init(deviceId, &stream)`：
     - `aclInit`
     - `aclrtSetDevice`
     - `aclrtCreateStream`
   - `CreateAclTensor<T>`：
     - 使用 `aclrtMalloc` 分配 device 内存
     - `aclrtMemcpy` 从 host 拷贝到 device
     - 计算连续 tensor 的 `strides`
     - 调用 `aclCreateTensor` 创建 `aclTensor*`

2. **主流程 main()**
   - 初始化 ACL runtime
   - 为每个输入/输出构造：
     - host 侧数据（`std::vector<T>`）
     - 对应的 shape（`std::vector<int64_t>`）
     - 调用 `CreateAclTensor(...)` 构造 `aclTensor*` 和 device addr
   - 获取 workspace 大小与执行器：
     - 调用 `aclnnYourOpGetWorkspaceSize(...)`
   - 如 `workspaceSize > 0`：
     - `aclrtMalloc` 分配 workspace
   - 调用真正算子：
     - `aclnnYourOp(workspaceAddr, workspaceSize, executor, stream);`
   - `aclrtSynchronizeStream(stream);`
   - 拷回输出并调用 `PrintOutResult` 打印结果
   - 销毁 tensor、释放 device 内存、销毁 stream、reset device、`aclFinalize`

### Agent 要点

- 为新 `aclnn_*` 示例时：
  - 完整 copy `test_aclnn_softmax_ops.cpp` 的结构，修改：
    - 头文件 include（`aclnnop/aclnn_xxx.h`）
    - 张量个数、shape、dtype 和填充数据
    - `aclnnXxxGetWorkspaceSize` / `aclnnXxx` 的函数名和参数列表
  - 保持：
    - 错误检查宏（`CHECK_RET`）和日志输出宏
    - 所有 `acl*` 资源的成对申请/释放

---

## 步骤六：测试与验证（如有 Python 前端）

如果项目中存在 Python 测试（例如 `op-plugin/test/test_custom_ops/test_*.py`）：

1. 使用现有测试文件作为模板：
   - 名称一般为 `test_npu_<op_name>_*.py`
   - 使用 NPU 设备，调用前端 API 封装的 op
2. 为新算子时：
   - 构造典型输入形状（包括边界场景）
   - 若有可对标的参考实现（如 CPU 版本或简单 Python 算法），用它计算期望输出
   - 断言：
     - shape、dtype 正确
     - 数值误差在合理范围内（尤其是量化/反量化场景）

---

## 对 agent 的额外约束

- **不要偷懒从零发明模式**：总是先查找并对齐相邻算子的实现与示例
- 修改任何已存在文件前：
  - 先完整阅读该文件，理解其在整体算子中的角色
- 对于涉及芯片支持 / 动态 shape / deterministic 的逻辑：
  - 优先保持现有算子的一致性，除非 bug 或需求要求改变
- 对示例和测试：
  - 宁可示例小而清晰（单个 shape、易于人工检查），也不要一开始就做过多复杂场景

---

## 简要使用示例

- **用户**：新增一个和 `grouped_matmul_finalize_routing` 类似，但 scale/bias 组合不同的 GMM 路由算子
- **Agent 行为（遵循本技能）**：
  1. 在 `gmm` 目录下找到 `grouped_matmul_finalize_routing_*` 相关文件并阅读
  2. 复制 `*_def.cpp`，改名和接口，调整输入/属性
  3. 复制 `op_kernel/grouped_matmul_finalize_routing.h` 中核心类，根据新需求调整 GM tensor 和反量化流程
  4. 参考相关 tiling/infershape 文件，确保 Graph 到 kernel 的参数映射正确
  5. 参考 `test_aclnn_softmax_ops.cpp` 写一个新的 `aclnn` 示例，并在需要时补充单测

