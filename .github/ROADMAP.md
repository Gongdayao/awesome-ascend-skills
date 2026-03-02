# Awesome Ascend Skills Roadmap

**Roadmap v1.0 — 2026** | 📅 Last Updated: 2026-03-02

---

## Overview

Awesome Ascend Skills 是面向华为昇腾 NPU 的结构化 AI Agent 知识库，涵盖从设备管理、模型转换、性能测试到推理部署的完整开发流程。本文档提供了所有 30 个 Skills 的概览信息，按功能类别组织，帮助 AI Agent 快速定位所需能力。

本文档包含以下内容：
- ✅ **9 个已完成 Skills** - 已实现并可投入使用
- 📋 **21 个待规划 Skills** - 计划中，需要进一步开发

---

## 🎯 使用指南

### 如何使用本 Roadmap
1. **根据场景选择类别**：查看各功能类别（基础环境 / 开发）
2. **定位具体 Skill**：浏览子类别下的 Skills 列表
3. **查看详细信息**：点击已实现 Skills 的链接阅读 SKILL.md

### 贡献新 Skill
如果您想为 Awesome Ascend Skills 贡献新的 Skill 或改进现有内容，请参考 [贡献指南](../README.md#贡献指南)。

---

## 📂 目录

- [1. 基础环境](#1-基础环境)
  - [1.1 基础指令](#11-基础指令)
  - [1.2 环境安装](#12-环境安装)
  - [1.3 基础测试](#13-基础测试)
- [2. 开发](#2-开发)
  - [2.1 通用框架](#21-通用框架)
  - [2.2 推理](#22-推理)
  - [2.3 训练](#23-训练)
  - [2.4 算子](#24-算子)
  - [2.5 Profiling](#25-profiling)

---

## 1. 基础环境

### 1.1 基础指令

#### **npu-smi** ✅ 已完成
NPU 设备管理命令工具，用于查询设备健康状态、监控温度/功耗、管理固件升级和虚拟化配置。支持查询设备信息、固件版本、温度、功耗、风扇转速等，是 NPU 开发的必备运维工具。

- **文档**: [npu-smi/SKILL.md](npu-smi/SKILL.md)
- **类型**: 运维
- **链接**: https://www.hiascend.com/document/detail/zh/canncommercial/81RC1/envdeployment/instg/instg_0045.html

#### **open-euler**
OpenEuler 操作系统相关技能，提供操作系统层面的昇腾设备支持、驱动配置和系统优化指南。帮助用户在 OpenEuler 环境下正确配置和优化 NPU 开发环境。

- **类型**: 系统配置
- **状态**: 📋 待规划

---

### 1.2 环境安装

#### **CANN (Compute Architecture for Neural Networks)**
华为昇腾 CANN 开发环境安装指南，提供 CANN 8.x 版本的多平台安装方案（容器、虚拟机、裸机），包含依赖项检查、安装步骤和验证方法。支持快速搭建完整的昇腾开发环境。

- **类型**: 开发环境
- **状态**: 📋 待规划

#### **HDK / Kernels**
HDK (Hardware Development Kit) 和自定义内核开发技能，指导开发者如何开发昇腾 NPU 硬件加速器、自定义算子和内核模块。适用于底层硬件优化和特殊场景的内核开发需求。

- **类型**: 底层开发
- **状态**: 📋 待规划

---

### 1.3 基础测试

#### **hccl-test** ✅ 已完成
HCCL (Huawei Collective Communication Library) 集合通信性能测试工具，提供集合通信带宽测试和 AllReduce/AllGather 等操作的性能基准测试。用于评估多卡分布式训练的通信性能，优化集群配置。

- **文档**: [hccl-test/SKILL.md](hccl-test/SKILL.md)
- **类型**: 测试
- **链接**: https://www.hiascend.com/document/detail/zh/canncommercial/81RC1/parameterconfiguration/paramconfig/paramconfig_0031.html

#### **ascend-docker** ✅ 已完成
昇腾 Docker 容器化开发环境配置技能，提供 NPU 设备映射、卷挂载、开发环境隔离的最佳实践。支持在 Docker 容器中运行昇腾应用，确保开发环境的一致性和可移植性。

- **文档**: [ascend-docker/SKILL.md](ascend-docker/SKILL.md)
- **类型**: 运维
- **链接**: https://www.hiascend.com/document/detail/zh/canncommercial/81RC1/dockerdevelopment/dockerdev/dockerdev_0001.html

#### **Ascend-dmi**
Ascend DMI (Device Management Interface) 技能，提供设备管理、状态监控和性能分析的高级工具。支持通过图形化界面或命令行管理 NPU 设备、查看性能指标和诊断问题。

- **类型**: 运维
- **状态**: 📋 待规划

#### **NPU 算子验证**
NPU 算子正确性验证工具，提供算子输入输出验证、精度对比和性能基准测试。帮助开发者验证自定义算子和标准算子的正确性，确保代码实现符合预期。

- **类型**: 测试
- **状态**: 📋 待规划

---

## 2. 开发

### 2.1 通用框架

#### **torch_npu** ✅ 已完成
PyTorch 昇腾扩展库，提供 PyTorch 在昇腾 NPU 上的完整支持。包含环境检查、部署指引、PyTorch 模型迁移到 NPU 的完整指南和常见问题解决方案。

- **文档**: [torch_npu/SKILL.md](torch_npu/SKILL.md)
- **类型**: 开发
- **链接**: https://www.hiascend.com/document/detail/zh/canncommercial/81RC1/nnoperational/nnoperational/nnoperational_0001.html

#### **OP-Plugin**
自定义算子插件开发技能，指导开发者如何通过插件机制扩展 PyTorch/框架的算子支持。适用于需要集成自定义算子或第三方算子的场景。

- **类型**: 开发
- **状态**: 📋 待规划

---

### 2.2 推理

#### **vllm-ascend** ✅ 已完成
vLLM 昇腾优化推理引擎，提供高效的批量推理、OpenAI 兼容 API 接口、量化模型支持和分布式推理能力。适用于大规模语言模型部署和推理优化场景。

- **文档**: [vllm-ascend/SKILL.md](vllm-ascend/SKILL.md)
- **类型**: 推理
- **链接**: https://docs.vllm.ai/en/stable/getting_started/quickstart.html

#### **msmodelslim** ✅ 已完成
msmodelslim 模型压缩量化工具，支持 W4A8/W8A8/W8A8S 量化、MoE/多模态模型压缩和精度自动调优。提供模型压缩、量化和优化的完整流程，是模型部署前的关键步骤。

- **文档**: [msmodelslim/SKILL.md](msmodelslim/SKILL.md)
- **类型**: 推理优化
- **链接**: https://github.com/Huawei-NOAH/AscendModelCompression

#### **ais-bench** ✅ 已完成
AISBench 基准测试工具，提供 AI 模型精度评估和性能测试功能。支持 15+ 个基准数据集（MMLU/GSM8K/MMMU 等）、性能压测、Function Call 测试和自定义数据集，是模型评估的必备工具。

- **文档**: [ais-bench/SKILL.md](ais-bench/SKILL.md)
- **类型**: 测试
- **链接**: https://www.hiascend.com/document/detail/zh/canncommercial/81RC1/toolkits/aisbench/aisbench_0001.html

#### **atc-model-converter** ✅ 已完成
ATC (Ascend Tensor Compiler) 模型转换工具，将 ONNX/TensorRT 模型转换为昇腾 .om 格式，支持模型推理、精度对比和 YOLO 端到端部署。提供模型压缩、量化、算子融合等功能。

- **文档**: [atc-model-converter/SKILL.md](atc-model-converter/SKILL.md)
- **类型**: 推理优化
- **链接**: https://www.hiascend.com/document/detail/zh/canncommercial/81RC1/modelconvert/conv/conv_0001.html

#### **Diffusers**
Diffusers 模型库昇腾优化技能，提供 Stable Diffusion、ControlNet 等 AIGC 模型的 NPU 推理支持。包含模型转换、优化和推理部署的最佳实践。

- **类型**: 推理
- **状态**: 📋 待规划

#### **sglang**
SGLang 推理框架昇腾优化技能，提供高性能大语言模型推理服务。支持长上下文、函数调用、多模态推理等高级功能。

- **类型**: 推理
- **状态**: 📋 待规划

#### **vllm-omni**
vllm-omni 多模态推理引擎昇腾优化技能，提供文本、图像、音频等多模态大模型的统一推理服务。支持多模态输入处理、跨模态对齐和多模态生成。

- **类型**: 推理
- **状态**: 📋 待规划

#### **vllm-benchmark**
vLLM 推理性能基准测试工具，专门针对 vLLM 推理引擎在昇腾 NPU 上的性能评估。提供 Throughput、Latency、TTFT 等关键指标的测试方法和优化建议。

- **类型**: 测试
- **状态**: 📋 待规划

#### **sglang-benchmark**
SGLang 推理性能基准测试工具，专门针对 SGLang 推理框架在昇腾 NPU 上的性能评估。提供长上下文、函数调用等场景的性能测试和对比分析。

- **类型**: 测试
- **状态**: 📋 待规划

#### **小模型**
轻量级模型昇腾优化技能，专注于压缩和优化小模型（如 MobileBERT、TinyBERT 等）在昇腾 NPU 上的推理性能。提供模型量化、剪枝和部署指南。

- **类型**: 推理
- **状态**: 📋 待规划

---

### 2.3 训练

#### **MindSpeed**
MindSpeed 训练框架昇腾优化技能，提供高性能分布式训练支持（数据并行、模型并行、流水线并行）。适用于大规模深度学习模型训练场景。

- **类型**: 训练
- **状态**: 📋 待规划

#### **MindSpore**
MindSpore 框架昇腾优化技能，提供从数据预处理、模型训练、模型评估到部署的全流程支持。包含模型转换、性能优化和部署指南。

- **类型**: 训练
- **状态**: 📋 待规划

#### **Verl**
RLHF 训练框架昇腾优化技能，提供基于 Reinforcement Learning from Human Feedback 的对齐训练支持。适用于大语言模型对齐和微调场景。

- **类型**: 训练
- **状态**: 📋 待规划

---

### 2.4 算子

#### **ascendc** ✅ 已完成
AscendC 算子开发工具，提供 CANN API 的详细示例和最佳实践。涵盖 FFN（前馈网络）、GMM（General Matrix Multiply）、MoE（Mixture of Experts）等 Transformer 核心算子的实现，是昇腾算子开发的标准参考。

- **文档**: [ascendc/SKILL.md](ascendc/SKILL.md)
- **类型**: 开发
- **链接**: https://www.hiascend.com/document/detail/zh/canncommercial/81RC1/nnoperational/nnoperational/nnoperational_0001.html

#### **Catlass**
自定义张量类开发技能，指导开发者如何扩展和优化张量数据结构，提升算子性能。适用于需要自定义张量数据类型的特殊场景。

- **类型**: 开发
- **状态**: 📋 待规划

#### **Triton**
Triton 内核开发昇腾优化技能，提供 Triton 语言与昇腾 NPU 的集成方案。支持在昇腾平台上编写和优化 Triton 内核，提升算子性能。

- **类型**: 开发
- **状态**: 📋 待规划

#### **TileLang-Ascend**
TileLang 昇腾优化技能，提供基于 Tile 模型的算子开发方法。支持高性能并行计算和自动优化。

- **类型**: 开发
- **状态**: 📋 待规划

---

### 2.5 Profiling

#### **推理 Profiling**
推理性能分析工具，提供推理模型的详细性能分析、延迟、吞吐量和资源占用分析。帮助识别性能瓶颈和优化方向。

- **类型**: Profiling
- **状态**: 📋 待规划

#### **训练 Profiling**
训练性能分析工具，提供训练过程的性能分析、显存占用、计算图分析和优化建议。适用于大规模训练性能调优。

- **类型**: Profiling
- **状态**: 📋 待规划

---

## 📊 进度统计

| 类别 | 已完成 | 待规划 | 总计 |
|------|--------|--------|------|
| 基础环境 | 3 | 4 | 7 |
| 开发 | 6 | 17 | 23 |
| **总计** | **9** | **21** | **30** |

---

## 🤝 贡献者

感谢所有为 Awesome Ascend Skills 贡献的开发者！

- **当前维护者**: Ascend AI Coding 社区
- **贡献指南**: [贡献指南](../README.md#贡献指南)
- **问题反馈**: [提交 Issue](https://github.com/ascend-ai-coding/awesome-ascend-skills/issues)

---

## 📖 相关资源

- [华为昇腾官方文档](https://www.hiascend.com/document)
- [CANN 开发指南](https://www.hiascend.com/document/detail/zh/canncommercial/)
- [vLLM 文档](https://docs.vllm.ai/)
- [MindSpore 文档](https://www.mindspore.cn/)
- [PyTorch 昇腾扩展](https://github.com/HuaweiAscend/pytorch)

---

## 📝 更新日志

### 2026-03-02
- ✅ 创建 Roadmap v1.0
- ✅ 完成 9 个已完成 Skills 的标注和链接
- 📋 规划 21 个待开发 Skills

---

**License**: MIT License | **Maintained by**: Ascend AI Coding Community
