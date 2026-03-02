# Draft: README & Rules Refactoring

## 需求概述
重构 README 和规则，包含：
1. Skill 安装（手动 & 自动）
2. 如何写 Skill
3. 如何提交 PR（需要 PR Template）

## 当前状态

### 现有文件
- ✅ README.md - 基础结构存在
- ✅ AGENTS.md - 已更新
- ✅ .github/workflows/validate-skills.yml - CI/CD
- ❌ CONTRIBUTING.md - 不存在
- ❌ PULL_REQUEST_TEMPLATE.md - 不存在
- ✅ skills/template/SKILL.md - 存在但不完善

### 研究进行中
- Explore agent: 分析 skill 写作模式
- Librarian agent: 查找官方文档和最佳实践

---

## 用户回答（已确认）

### Q1: 目标受众
**✅ 两者兼顾（平衡）**
- 需要同时包含使用指南和贡献指南
- README 需要分段展示不同内容

### Q2: PR 检查项
**✅ 完整检查**
- 基础检查（name 匹配、description 长度、frontmatter）
- 链接验证（内部链接可访问）
- 无 TODO 占位符
- 已添加到 marketplace.json

### Q3: 文档组织
**✅ 单文件 README**
- 所有内容在 README.md
- 使用目录导航
- 不需要单独的 CONTRIBUTING.md

### Q4: Skill 模板
**✅ 完整示例**
- 一个完整的示例 Skill
- 包含注释说明每个字段
- 展示最佳实践

---

## 决策
- [x] 目标受众：两者兼顾
- [x] PR 检查项：完整检查
- [x] 文档组织：单文件 README
- [x] Skill 模板：完整示例

---

## 研究发现

### 代码库模式（Explore Agent 结果）

**1. 必需的 Frontmatter 字段**
- `name`: 必须匹配目录名，kebab-case
- `description`: 最少 20 字符，需包含何时使用
- `keywords`: 可选，推荐用于中文/双语 skill

**2. 验证规则**
- ERROR: 缺少 name/description、name 不匹配目录、frontmatter 格式错误
- WARNING: description <20 字符、包含 TODO、内容太短

**3. 目录结构**
```
skill-name/
├── SKILL.md      # 核心内容（≤500 行）
├── references/   # 详细文档（可选）
├── scripts/      # 可执行脚本（可选）
└── assets/       # 配置模板等（可选）
```

**4. 命名规范**
- 目录: lowercase-with-hyphens
- Skill name: 必须匹配目录名
- 脚本: kebab-case.sh / snake_case.py

### 官方文档模式（Librarian Agent 结果）

**1. Description 最重要**
- 结构: `[What] + [When] + [Key capabilities]`
- 示例: "Analyzes Figma files. Use when user uploads .fig, asks for design specs."

**2. 推荐的 SKILL.md 结构**
- Quick Start (最常用命令)
- Instructions (分步骤)
- Examples (使用场景)
- Troubleshooting (常见错误)

**3. PR Template 关键检查项**
- name 匹配目录（kebab-case）
- Description 包含触发条件
- 无 README.md 在 skill 目录
- SKILL.md 大小写正确
- YAML frontmatter 有效

## 最终确认（第二轮）

### Q5: README 语言
**✅ 仅中文**
- 所有文档只用中文

### Q6: 安装工具
**✅ 多工具支持**
- Claude Code
- OpenCode
- Cursor
- Trae CN
- Trae
- Codex

### Q7: Skill 示例选择
**✅ 创建新示例（skill-creator）**
- 使用 skill-creator 作为完整示例
- 展示如何写一个 Skill
- 包含详细注释和最佳实践
