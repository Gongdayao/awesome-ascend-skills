# Draft: Awesome Ascend Skills Roadmap

## Context

Creating a comprehensive roadmap document for the awesome-ascend-skills repository - a knowledge base repository structured as flat AI Skills for Huawei Ascend NPU development.

## Current Repository State

### Existing Skills (9 Complete)

| Skill | Category | SKILL.md Lines | Status | Notes |
|-------|----------|---------------|---------|-------|
| npu-smi | Operations | 211 | ✅ Complete | Device management |
| hccl-test | Testing | 422 | ✅ Complete | HCCL performance testing |
| atc-model-converter | Development | 342 | ✅ Complete | ONNX → OM conversion |
| ascend-docker | Operations | 184 | ✅ Complete | Docker containerization |
| msmodelslim | Development | 392 | ✅ Complete | Model quantization |
| ais-bench | Testing | 392 | ✅ Complete | AI model evaluation |
| ascendc | Development | 1138 | ✅ Complete | AscendC operator dev |
| torch_npu | Development | 142 | ✅ Complete | PyTorch NPU extension |
| vllm-ascend | Development | 478 | ✅ Complete | vLLM inference |

### Documentation Patterns

All skills follow consistent structure:
```
skill-name/
├── SKILL.md (YAML frontmatter: name, description, keywords)
├── references/ (detailed docs)
└── scripts/ (executable utilities)
```

- Progressive disclosure: Core content in SKILL.md (≤500 lines), details in references/
- Bilingual support: Chinese content encouraged
- Naming: kebab-case directories and files

### No Existing Roadmap Document

**Current State**: No ROADMAP.md file exists in the repository.

## User's Proposed Roadmap Structure

The user provided a comprehensive hierarchical structure covering end-to-end Ascend NPU development:

### 1. 基础环境

#### 1.1 基础指令
- ✅ npu-smi (已完成)
- open-euler 基础指令 (待添加)

#### 1.2 环境安装
- CANN(8.5 之前与之后)
- HDK/Kernels

#### 1.3 基础测试
- ✅ hccl-test 打流 (已完成)
- ✅ docker 搭建 (已完成 - ascend-docker)
- ascend-dmi 压测
- NPU 算子单用例验证

### 2. 开发

#### 2.1 通用框架
- ✅ Torch-NPU (已完成 - torch_npu, 待扩展)
  - PyTorch 算子 API (待规划)
  - ... (待规划)
- OP-Plugin
  - 算子接入
  - ... (待规划)

#### 2.2 推理
- Diffusers (部署/适配/测试)
- ✅ Vllm-Ascend (已完成)
- Vllm-Omni (部署/适配/测试)
- Sglang (部署/适配/测试)
- Vllm-Benchmark
- ✅ Ais-Benchmark (已完成 - ais-bench)
- Sglang-Benchmark
- 小模型
  - onnx
  - pt

#### 2.3 训练
- MindSpeed (部署/适配/测试)
- MindSpore (部署/适配/测试)
- Verl (部署/适配/测试)

#### 2.4 算子
- ✅ AscendC (已完成)
- Catlass
- Triton
- TileLang-Ascend

#### 2.5 Profiling
- 推理 (采集/分析)
- 训练 (采集/分析)

## Decisions to Make

1. **Roadmap Format**: Should the roadmap be:
   - A markdown document in the root directory (ROADMAP.md)?
   - A dedicated section in README.md?
   - A separate docs/roadmap.md file?

2. **Skill Naming Convention**: For the proposed skills like "open-euler", "mindspore", "verl":
   - Should they follow kebab-case: `open-euler`, `mindspore`, `verl`, `sglang`?
   - Or follow the pattern with dash: `open-euler-basic`, `vllm-omni`, `sglang-inference`?

3. **Roadmap Organization**: Should skills be:
   - Grouped by category (Environment, Inference, Training, Profiling)?
   - Listed with priorities (P0, P1, P2)?
   - Organized by completion status (Complete, In Progress, Planned)?

4. **Skill Description Requirements**: For each planned skill, do we need:
   - Brief description in the roadmap?
   - Detailed scope definition?
   - Priority level and estimated effort?
   - Dependencies on other skills?

5. **GitHub Integration**: Should the roadmap include:
   - Links to GitHub issues for tracking?
   - Milestones for releases?
   - Contribution guidelines for each skill?

## Technical Considerations

1. **SKILL.md Size Limits**: The current guidelines recommend ≤500 lines. Some existing skills exceed this (ascendc: 1138 lines, vllm-ascend: 478 lines). Should the roadmap mention this constraint or adjust it?

2. **Skill Dependencies**: Many skills have dependencies (e.g., inference skills require CANN environment). Should the roadmap explicitly document these dependencies?

3. **Testing Requirements**: The repository has strong testing infrastructure. Should the roadmap include:
   - Test requirements for each skill?
   - QA process guidelines?

## Open Questions

1. What is the target timeline for completing the roadmap?
2. Are there specific priorities (which skills should be implemented first)?
3. Should the roadmap include "nice-to-have" vs "must-have" skills?
4. Are there any skills that should be explicitly marked as "out of scope"?
5. Should the roadmap include maintenance/updates for existing skills?



## User Decisions Confirmed

### Roadmap Format
- **Location**: Upload to GitHub Issue (not a markdown file in repo)
- **Organization**: Priority-based (P0, P1, P2)
- **Detail Level**: Brief (Skill Name + Description)
- **Release Strategy**: Continuous delivery (no milestone releases)
- **Contribution Model**: Open issues, first-come-first-served

### Priority Framework

**P0 (Critical Path - Foundation Skills):**
- Required for other skills to work
- Core environment setup
- Basic NPU capabilities

**P1 (High Priority - Core Workflows):**
- Common developer workflows (inference, training, operators)
- Popular frameworks (Diffusers, Sglang, MindSpore)

**P2 (Medium Priority - Specialized Tools):**
- Specialized tooling (Profiling, advanced operators)
- Optimization tools (Triton, TileLang)