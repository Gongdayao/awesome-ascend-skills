# README & PR Template 重构计划

## TL;DR

> **快速摘要**: 重构 README.md（单文件，中文，包含安装指南+贡献指南），创建 PR Template（完整检查项），新建 skill-creator 作为完整示例 Skill。
> 
> **交付物**:
> - 重构后的 README.md
> - .github/PULL_REQUEST_TEMPLATE.md
> - skills/skill-creator/SKILL.md（新示例）
> - .claude-plugin/marketplace.json（更新 skill-creator 条目）
> 
> **预估工作量**: Short
> **并行执行**: YES - 3 waves
> **关键路径**: Task 1 → Task 2 → Task 3

---

## Context

### 原始需求
用户需要重构 README 和规则，包含：
1. Skill 安装（手动 & 自动）
2. 如何写 Skill
3. 如何提交 PR（需要 PR Template）

### 访谈摘要
**关键讨论**:
- 目标受众: 两者兼顾（使用者和贡献者）
- PR 检查项: 完整检查（基础 + 链接 + TODO + marketplace.json）
- 文档组织: 单文件 README，使用目录导航
- Skill 模板: 完整示例（使用 skill-creator）
- 语言: 仅中文
- 安装工具: Claude Code, OpenCode, Cursor, Trae CN, Trae, Codex

**研究发现**:
- Frontmatter: name（匹配目录）, description（≥20 字符）, keywords（可选）
- 验证规则: ERROR（缺少字段）+ WARNING（内容问题）
- 推荐结构: Quick Start + Instructions + Examples + Troubleshooting

### 自我审查（Metis 替代）
**识别的缺口**（已解决）:
- 护栏: 明确 README 长度限制，避免过于冗长
- 范围边界: 不修改 AGENTS.md，不创建 CONTRIBUTING.md
- 假设: 假设 Trae CN/Trae 工具已支持 skills 安装

### 高精度审核结果（已修复）
**修复的问题**:
- ✅ 路径决策：明确创建 `skills/skill-creator/` 与现有 `skills/skills/skill-creator/` 分离
- ✅ 递归依赖：移除 `skill-creator` skill 依赖，改用 `doc-coauthoring`
- ✅ Final Tasks：添加完整的 Acceptance Criteria 和 Evidence
- ✅ marketplace.json：Task 3 新增更新 marketplace.json 的要求

---

## Work Objectives

### 核心目标
创建完整的中文文档系统，帮助用户安装 Skill 并指导开发者贡献新 Skill。

### 具体交付物
- `README.md` - 重构后的主文档（中文）
- `.github/PULL_REQUEST_TEMPLATE.md` - PR 模板
- `skills/skill-creator/SKILL.md` - 完整示例 Skill
- `.claude-plugin/marketplace.json` - 更新 skill-creator 条目

### 完成定义
- [ ] README.md 包含目录导航、安装指南、贡献指南
- [ ] PR Template 包含完整检查项（checkbox 格式）
- [ ] skill-creator Skill 可以作为教学示例使用
- [ ] 运行 `python3 scripts/validate_skills.py` 通过

### Must Have
- README 目录导航
- 安装指南（6 种工具）
- 贡献指南（如何写 Skill）
- PR Template 完整检查项
- skill-creator 完整示例

### Must NOT Have（护栏）
- 不修改 AGENTS.md（已更新）
- 不创建单独的 CONTRIBUTING.md
- 不修改现有 Skill 的内容
- 不添加英文版本（仅中文）
- 不修改 `skills/skills/skill-creator/`（现有工具集）

---

## Verification Strategy

### 测试决策
- **Infrastructure exists**: YES（validate_skills.py）
- **Automated tests**: Tests-after（验证脚本）
- **Framework**: Python validation script

### QA Policy
每个任务包含 Agent 执行的 QA 场景。

---

## Execution Strategy

### Parallel Execution Waves

```
Wave 1 (Start Immediately — 基础结构):
├── Task 1: 重构 README.md [quick]
└── Task 2: 创建 PR Template [quick]

Wave 2 (After Wave 1 — 示例 Skill):
└── Task 3: 创建 skill-creator SKILL.md [unspecified-high]

Wave FINAL (After ALL tasks — 验证):
├── Task F1: 运行验证脚本 [quick]
├── Task F2: 检查 README 目录链接 [quick]
└── Task F3: 验证 PR Template 格式 [quick]

Critical Path: Task 1 → Task 3 → F1-F3
Parallel Speedup: 2 tasks in Wave 1
Max Concurrent: 2
```

### Agent Dispatch Summary
- **Wave 1**: 2 tasks → `quick`
- **Wave 2**: 1 task → `unspecified-high`
- **FINAL**: 3 tasks → `quick`

---

## TODOs

- [ ] 1. 重构 README.md

  **What to do**:
  - 创建新的 README.md 结构
  - 添加目录导航
  - 添加安装指南（6 种工具：Claude Code, OpenCode, Cursor, Trae CN, Trae, Codex）
  - 添加 Skill 列表表格
  - 添加贡献指南（如何写 Skill）
  - 添加如何提交 PR 章节

  **Must NOT do**:
  - 不修改 AGENTS.md
  - 不创建单独的 CONTRIBUTING.md
  - 不添加英文版本

  **Recommended Agent Profile**:
  - **Category**: `writing`
  - **Skills**: [`doc-coauthoring`]
    - `doc-coauthoring`: 文档写作和结构化

  **Parallelization**:
  - **Can Run In Parallel**: YES
  - **Parallel Group**: Wave 1 (with Task 2)
  - **Blocks**: Task 3
  - **Blocked By**: None

  **References**:
  - `README.md` - 当前 README 结构
  - `AGENTS.md:69-135` - Code Style Guidelines
  - `scripts/validate_skills.py` - 验证规则
  - `.claude-plugin/marketplace.json` - Skill 列表

  **Acceptance Criteria**:
  - [ ] README 包含目录导航（使用 `[TOC]` 或手动目录）
  - [ ] README 包含 6 种工具的安装说明
  - [ ] README 包含 Skill 列表表格
  - [ ] README 包含贡献指南
  - [ ] README 语言为中文

  **QA Scenarios**:
  ```
  Scenario: README 结构验证
    Tool: Bash
    Steps:
      1. 检查 README.md 文件存在
      2. grep 检查包含 "目录" 或 "Table of Contents"
      3. grep 检查包含 "安装" 或 "Installation"
      4. grep 检查包含 "贡献" 或 "Contributing"
    Expected Result: 所有检查通过
    Evidence: .sisyphus/evidence/task-1-readme-structure.txt
  ```

  **Commit**: YES
  - Message: `docs: refactor README with installation and contribution guides`
  - Files: `README.md`

---

- [ ] 2. 创建 PR Template

  **What to do**:
  - 创建 `.github/PULL_REQUEST_TEMPLATE.md`
  - 包含完整检查项（checkbox 格式）
  - 包含 Skill 描述模板
  - 包含测试检查项

  **Must NOT do**:
  - 不使用英文（仅中文）
  - 不添加过多复杂的检查项

  **Recommended Agent Profile**:
  - **Category**: `writing`
  - **Skills**: []

  **Parallelization**:
  - **Can Run In Parallel**: YES
  - **Parallel Group**: Wave 1 (with Task 1)
  - **Blocks**: None
  - **Blocked By**: None

  **References**:
  - `.github/workflows/validate-skills.yml` - CI 检查项
  - `scripts/validate_skills.py:29-75` - 验证规则

  **Acceptance Criteria**:
  - [ ] 文件位于 `.github/PULL_REQUEST_TEMPLATE.md`
  - [ ] 包含 checkbox 格式的检查项
  - [ ] 包含以下检查项：
    - [ ] `name` 匹配目录名
    - [ ] `description` ≥20 字符
    - [ ] frontmatter 格式正确
    - [ ] 无 TODO 占位符
    - [ ] 内部链接可访问
    - [ ] 已添加到 marketplace.json
    - [ ] 已更新 README.md

  **QA Scenarios**:
  ```
  Scenario: PR Template 验证
    Tool: Bash
    Steps:
      1. 检查文件存在于 .github/PULL_REQUEST_TEMPLATE.md
      2. grep 检查包含 checkbox 格式 "- [ ]"
      3. grep 检查包含 "name"
      4. grep 检查包含 "description"
    Expected Result: 所有检查通过
    Evidence: .sisyphus/evidence/task-2-pr-template.txt
  ```

  **Commit**: YES
  - Message: `docs: add PR template with skill checklist`
  - Files: `.github/PULL_REQUEST_TEMPLATE.md`

---

- [ ] 3. 创建 skill-creator SKILL.md

  **What to do**:
  - 创建 `skills/skill-creator/` 目录
  - 创建 `SKILL.md` 文件
  - 包含完整的 frontmatter（带注释说明）
  - 包含 Quick Start 示例
  - 包含最佳实践说明
  - 包含常见错误和解决方案
  - 作为教学示例使用
  - 更新 `.claude-plugin/marketplace.json`

  **Must NOT do**:
  - 不与现有的 skills/skills/skill-creator/ 冲突
  - 不使用英文（仅中文）
  - 不修改现有 Skill 的内容

  **Recommended Agent Profile**:
  - **Category**: `unspecified-high`
  - **Skills**: [`doc-coauthoring`]
    - `doc-coauthoring`: 文档结构和写作指导
  
  **Path Decision**: 创建 `skills/skill-creator/` (root level) 作为教学示例
  **Rationale**: 与 `skills/skills/skill-creator/`（完整工具集）分离，保持简洁示例

  **Parallelization**:
  - **Can Run In Parallel**: NO
  - **Parallel Group**: Wave 2
  - **Blocks**: F1-F3
  - **Blocked By**: Task 1

  **References**:
  - `skills/template/SKILL.md` - 基础模板
  - `npu-smi/SKILL.md` - 完整示例
  - `AGENTS.md:71-98` - SKILL.md 格式指南
  - `.sisyphus/drafts/readme-refactoring.md` - 研究发现

  **Acceptance Criteria**:
  - [ ] 文件位于 `skills/skill-creator/SKILL.md`
  - [ ] frontmatter 包含 name, description, keywords
  - [ ] 包含详细注释说明每个字段的作用
  - [ ] 包含 Quick Start 章节
  - [ ] 包含最佳实践章节
  - [ ] 包含常见错误章节
  - [ ] 已添加到 `.claude-plugin/marketplace.json`
  - [ ] 运行 `python3 scripts/validate_skills.py` 通过

  **QA Scenarios**:
  ```
  Scenario: skill-creator 验证
    Tool: Bash
    Steps:
      1. python3 scripts/validate_skills.py
      2. 检查输出无 ERROR
      3. grep 检查 SKILL.md 包含 "Quick Start"
      4. grep 检查 SKILL.md 包含 "最佳实践"
    Expected Result: 验证通过，内容完整
    Evidence: .sisyphus/evidence/task-3-skill-creator.txt
  ```

  **Commit**: YES
  - Message: `feat: add skill-creator as complete example`
  - Files: `skills/skill-creator/SKILL.md`, `.claude-plugin/marketplace.json`

---

## Final Verification Wave

**Pre-flight**: `mkdir -p .sisyphus/evidence`

- [ ] F1. 运行验证脚本
  
  **What to do**: 执行验证脚本并记录结果
  ```bash
  python3 scripts/validate_skills.py
  ```
  **Acceptance Criteria**:
  - [ ] 输出包含 "Validation PASSED" 或无 ERROR
  **Evidence**: `.sisyphus/evidence/final-validation.txt`

- [ ] F2. 检查 README 目录链接
  
  **What to do**: 验证 README 中所有内部链接有效
  ```bash
  grep -E '\[.*\]\(#.*\)' README.md
  ```
  **Acceptance Criteria**:
  - [ ] 所有锚点链接目标存在
  **Evidence**: `.sisyphus/evidence/final-readme-links.txt`

- [ ] F3. 验证 PR Template 格式
  
  **What to do**: 确认 PR Template 包含必要的检查项
  ```bash
  cat .github/PULL_REQUEST_TEMPLATE.md
  ```
  **Acceptance Criteria**:
  - [ ] 包含 checkbox 格式 `- [ ]`
  - [ ] 内容为中文
  **Evidence**: `.sisyphus/evidence/final-pr-template.txt`

---

## Commit Strategy

- **Commit 1**: `docs: refactor README with installation and contribution guides` — README.md
- **Commit 2**: `docs: add PR template with skill checklist` — .github/PULL_REQUEST_TEMPLATE.md
- **Commit 3**: `feat: add skill-creator as complete example` — skills/skill-creator/SKILL.md, .claude-plugin/marketplace.json

---

## Success Criteria

### 验证命令
```bash
python3 scripts/validate_skills.py  # Expected: ✅ Validation PASSED!
```

### 最终检查清单
- [ ] README.md 包含目录导航
- [ ] README.md 包含 6 种工具的安装说明
- [ ] README.md 包含贡献指南
- [ ] PR Template 包含完整检查项
- [ ] skill-creator SKILL.md 可以作为教学示例
- [ ] 所有验证脚本通过
