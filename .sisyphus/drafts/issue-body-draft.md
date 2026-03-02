# Roadmap: Awesome Ascend Skills (2026)

## 简介

**Awesome Ascend Skills** 是面向华为昇腾 NPU 的结构化 AI Agent 知识库，以 Skill 模块形式组织昇腾开发场景的完整能力。每个 Skill 是独立的 Agent 能力单元，支持 Claude Code、OpenCode、Cursor、Trae、Codex 等多种 AI 编程工具。

本 Roadmap 定义了项目未来发展的完整路径，覆盖昇腾端到端开发流程：从 NPU 设备管理、容器环境配置、模型转换优化，到性能测试、量化压缩、推理部署的全链路能力。

**Roadmap 目标**：
- 📚 提供结构化的昇腾开发知识体系
- 🚀 支持多种 AI 编程工具的无缝集成
- 🔄 建立可追踪的 Skill 开发进度管理
- 🤝 鼓励社区贡献，共同完善昇腾生态

---

## 已完成的 Skills

以下 9 个 Skills 已完成开发并通过验证：

| Skill | 类别 | 描述 |
|-------|------|------|
| [npu-smi](npu-smi/SKILL.md) | 运维 | NPU 设备管理：健康状态查询、温度/功耗监控、固件升级、虚拟化配置、证书管理 |
| [hccl-test](hccl-test/SKILL.md) | 测试 | HCCL 集合通信性能测试：带宽测试、AllReduce/AllGather 等集合操作基准测试 |
| [atc-model-converter](atc-model-converter/SKILL.md) | 开发 | ATC 模型转换：ONNX 转 .om 格式、OM 推理、精度对比、YOLO 端到端部署 |
| [ascend-docker](ascend-docker/SKILL.md) | 运维 | Docker 容器配置：NPU 设备映射、卷挂载、开发环境隔离 |
| [msmodelslim](msmodelslim/SKILL.md) | 开发 | 模型压缩量化：W4A8/W8A8/W8A8S 量化、MoE/多模态模型支持、精度自动调优 |
| [vllm-ascend](vllm-ascend/SKILL.md) | 开发 | vLLM 推理引擎：离线批推理、OpenAI 兼容 API、量化模型服务、分布式推理 |
| [ais-bench](ais-bench/SKILL.md) | 测试 | AI 模型评估工具：精度评估（MMLU/GSM8K/MMMU 等 15+ 基准）、性能压测、Function Call |
| [ascendc](ascendc/SKILL.md) | 开发 | AscendC 算子开发：FFN/GMM/MoE 等 Transformer 算子实现、CANN API 示例 |
| [torch_npu](torch_npu/SKILL.md) | 开发 | PyTorch 昇腾扩展：环境检查、部署指引、PyTorch 迁移到 NPU 的完整指南 |

---

## 待规划的 Skills

以下 21 个 Skills 按类别组织，等待社区开发：

### 🏗️ 基础环境

#### 基础指令
- [ ] [ascend-info](ascend-info/SKILL.md) - 昇腾系统信息查询：版本、驱动、固件、环境变量
- [ ] [ascend-env-check](ascend-env-check/SKILL.md) - 环境检查脚本：依赖验证、NPU 检测、配置验证

#### 环境安装
- [ ] [cann-install](cann-install/SKILL.md) - CANN 安装指南：版本选择、依赖安装、配置验证
- [ ] [driver-install](driver-install/SKILL.md) - NPU 驱动安装：驱动选择、安装步骤、版本兼容性
- [ ] [docker-ascend](docker-ascend/SKILL.md) - 昇腾 Docker 环境：多版本共存、镜像构建、GPU/NPU 混合

### 🔧 开发工具

#### 算子开发
- [ ] [ascendc-tutorials](ascendc-tutorials/SKILL.md) - AscendC 入门教程：数据加载、内存管理、算子实现
- [ ] [ascendc-advanced](ascendc-advanced/SKILL.md) - AscendC 高级特性：异步执行、流水线、混合精度

#### 模型开发
- [ ] [atc-optimization](atc-optimization/SKILL.md) - ATC 优化技巧：算子融合、模型压缩、性能调优
- [ ] [custom-op-development](custom-op-development/SKILL.md) - 自定义算子开发：从原理到实现
- [ ] [model-conversion-guide](model-conversion-guide/SKILL.md) - 模型转换实战：常见问题、错误排查、最佳实践

### 🧪 测试验证

#### 性能测试
- [ ] [ascend-benchmark](ascend-benchmark/SKILL.md) - 昇腾性能基准测试：吞吐量、延迟、GPU 加速对比
- [ ] [accuracy-check](accuracy-check/SKILL.md) - 精度验证工具：模型对比、误差分析、可视化

#### 压力测试
- [ ] [hccl-stress-test](hccl-stress-test/SKILL.md) - HCCL 压力测试：大规模集群、通信瓶颈分析
- [ ] [npu-stress-test](npu-stress-test/SKILL.md) - NPU 压力测试：长时间运行、内存泄漏检测、异常处理

### 🚀 推理部署

#### 推理引擎
- [ ] [openvino-ascend](openvino-ascend/SKILL.md) - OpenVINO 昇腾后端：模型优化、推理加速、部署指南
- [ ] [tensorrt-ascend](tensorrt-ascend/SKILL.md) - TensorRT 昇腾适配：模型转换、性能优化、部署实战
- [ ] [onnxruntime-ascend](onnxruntime-ascend/SKILL.md) - ONNX Runtime 昇腾：推理引擎集成、模型加载、推理调用

#### 部署工具
- [ ] [model-serving](model-serving/SKILL.md) - 模型服务化：RESTful API、gRPC 服务、容器化部署
- [ ] [model-deployment](model-deployment/SKILL.md) - 模型部署指南：生产环境、监控告警、性能调优
- [ ] [model-optimization](model-optimization/SKILL.md) - 模型优化实践：量化、剪枝、蒸馏、知识蒸馏

### 📊 监控运维

#### 系统监控
- [ ] [npu-monitor](npu-monitor/SKILL.md) - NPU 监控工具：实时监控、日志分析、异常告警
- [ ] [system-health](system-health/SKILL.md) - 系统健康检查：资源监控、性能分析、故障排查

#### 问题诊断
- [ ] [ascend-troubleshooting](ascend-troubleshooting/SKILL.md) - 昇腾问题诊断：常见错误、解决方案、调试技巧
- [ ] [log-analysis](log-analysis/SKILL.md) - 日志分析工具：日志收集、解析、可视化、告警规则

### 🛠️ 高级特性

#### 多模态支持
- [ ] [vision-model-deploy](vision-model-deploy/SKILL.md) - 视觉模型部署：图像分类、目标检测、图像分割
- [ ] [audio-model-deploy](audio-model-deploy/SKILL.md) - 音频模型部署：语音识别、语音合成、音频处理

#### 边缘部署
- [ ] [edge-deployment](edge-deployment/SKILL.md) - 边缘部署指南：小模型优化、低功耗部署、实时推理
- [ ] [iot-deployment](iot-deployment/SKILL.md) - IoT 部署方案：嵌入式 NPU、边缘计算、设备管理

---

## 如何贡献

欢迎为 Awesome Ascend Skills 贡献新的 Skill 或改进现有内容！

### 贡献流程

1. **Fork 仓库**：点击 GitHub 页面右上角的 Fork 按钮
2. **克隆 Fork**：
   ```bash
   git clone https://github.com/YOUR_USERNAME/awesome-ascend-skills.git
   cd awesome-ascend-skills
   ```
3. **创建分支**：
   ```bash
   git checkout -b feat/your-skill-name
   # 或
   git checkout -b fix/description-of-fix
   ```
4. **开发 Skill**：
   - 创建 Skill 目录并编写 `SKILL.md`
   - 遵循[贡献指南](README.md#贡献指南)
5. **本地验证**：
   ```bash
   python3 scripts/validate_skills.py
   ```
6. **提交 PR**：按照[提交 PR 指南](README.md#提交-pr)

### 贡献类型

- ✨ **新 Skill 开发**：为 Roadmap 中的待规划 Skills 提交完整的实现
- 🐛 **Bug 修复**：修复现有 Skills 中的错误或问题
- 📝 **文档改进**：完善现有 Skills 的文档、示例和最佳实践
- 📚 **教程编写**：添加入门教程、进阶指南、案例研究
- 🔧 **脚本开发**：创建实用的辅助脚本和工具

### 贡献检查清单

在提交 PR 前，请确保：

- [ ] `name` 与目录名一致
- [ ] `description` 不少于 20 个字符
- [ ] SKILL.md 有有效的 YAML frontmatter（以 `---` 开始和结束）
- [ ] 内部链接可正常访问
- [ ] 无 `[TODO]` 占位符
- [ ] 已添加到 `.claude-plugin/marketplace.json`
- [ ] 已添加到 README.md 的 Skill 列表
- [ ] 运行 `python3 scripts/validate_skills.py` 通过

详细的贡献指南请参考：[README.md - 贡献指南](README.md#贡献指南)

---

## 相关资源

### 官方文档

- [华为昇腾官方文档](https://www.hiascend.com/document)
- [CANN 开发指南](https://www.hiascend.com/document/detail/zh/canncommercial/)
- [npu-smi 命令参考](https://www.hiascend.com/document/detail/zh/canncommercial/81RC1/envdeployment/instg/instg_0045.html)

### 技术社区

- [华为昇腾社区](https://www.hiascend.com/forum)
- [CANN GitHub](https://github.com/HuaweiAscend/cann)
- [昇腾 AI Coder 指南](https://gitee.com/ascend/CoderGuide)

### 工具链

- [CANN Toolkit](https://www.hiascend.com/document/detail/zh/canncommercial/81RC1/quickstart/start_01_0001.html)
- [ATC 工具](https://www.hiascend.com/document/detail/zh/canncommercial/81RC1/tool_development/compile/compile_01_0001.html)
- [AscendC 开发工具](https://www.hiascend.com/document/detail/zh/canncommercial/81RC1/kernel/py/ascendc/ascendc_01_0001.html)

### 示例项目

- [MindSpore](https://www.hiascend.com/document/detail/zh/mindspore/development/tensor/develop_01_0001.html)
- [PyTorch 昇腾扩展](https://gitee.com/ascend/pytorch)
- [TorchScript 昇腾](https://gitee.com/ascend/torchscript)
- [OpenVINO 昇腾后端](https://github.com/openvinotoolkit/openvino/tree/master/inference-engine/intel_cpu_extensions/ops/ascend)

---

## 路线图

- **2026 Q1**：完成基础环境类 Skills（5 个）
- **2026 Q2**：完成开发工具类 Skills（6 个）
- **2026 Q3**：完成测试验证类 Skills（5 个）
- **2026 Q4**：完成推理部署和监控运维类 Skills（5 个）
- **2027 Q1**：完成高级特性类 Skills（4 个）

---

**标签**: `roadmap`, `planning`, `development`

---

*Last updated: 2026-03-02*
