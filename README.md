# Universal Coding Skills

给编程助手（Codex、OpenCode）使用的专业技能库。让助手在特定任务中遵循经过验证的方法论，而不是自由发挥。

## 安装

```bash
# Clone
git clone git@github.com:jjjojoj/universal-coding-skills.git

# 安装到 Codex
for skill in $(ls skills/engineering skills/productivity); do
  cp -r "skills/engineering/$skill" ~/.codex/skills/ 2>/dev/null
  cp -r "skills/productivity/$skill" ~/.codex/skills/ 2>/dev/null
done

# 安装到 OpenCode
mkdir -p ~/.config/opencode/skills
for skill in $(ls skills/engineering skills/productivity); do
  cp -r "skills/engineering/$skill" ~/.config/opencode/skills/ 2>/dev/null
  cp -r "skills/productivity/$skill" ~/.config/opencode/skills/ 2>/dev/null
done
```

## Skill 索引

### Engineering（工程）

| Skill | 用途 | 触发条件 |
|-------|------|---------|
| [diagnose](skills/engineering/diagnose/) | 系统化调试：先建反馈循环，再定位根因 | 有 bug 需要调试 |
| [prototype](skills/engineering/prototype/) | 构建可丢弃代码回答设计问题 | 需要验证 UI 概念或逻辑方案 |
| [tdd](skills/engineering/tdd/) | 行为驱动测试开发，垂直切片 | 实现需要测试保护的功能 |
| [zoom-out](skills/engineering/zoom-out/) | 画高层代码地图，理解模块关系 | 不熟悉的代码区域 |
| [triage](skills/engineering/triage/) | Issue 分类和状态管理 | 处理 issue backlog |
| [to-prd](skills/engineering/to-prd/) | 从对话上下文合成 PRD | 设计讨论需要文档化 |
| [to-issues](skills/engineering/to-issues/) | 把计划拆成垂直切片 issue | PRD 需要分解为任务 |
| [grill-with-docs](skills/engineering/grill-with-docs/) | 对照项目文档审阅方案 | 需要接地气的设计审阅 |
| [improve-codebase-architecture](skills/engineering/improve-codebase-architecture/) | 找架构加深机会 | 代码结构需要改进 |

### Productivity（效率）

| Skill | 用途 | 触发条件 |
|-------|------|---------|
| [caveman](skills/productivity/caveman/) | 超精简回复模式，省 ~75% token | 需要省 token |
| [grill-me](skills/productivity/grill-me/) | 逐个问题审阅设计方案 | 需要找方案漏洞 |
| [write-a-skill](skills/productivity/write-a-skill/) | 创建新 skill 的指南 | 需要编写新 skill |

## Skill 结构

```
skill-name/
├── SKILL.md           # 主文件（必须，包含 YAML frontmatter）
├── REFERENCE.md       # 参考文档（按需）
├── EXAMPLES.md        # 示例（按需）
└── scripts/           # 工具脚本（按需）
```

### SKILL.md Frontmatter

每个 SKILL.md 必须包含 YAML frontmatter：

```yaml
---
name: skill-name
description: 一句话说明功能。Use when [触发条件]。
---
```

`description` 是助手判断是否加载该 skill 的唯一依据，必须精确。

## 来源

基于 [mattpocock/skills](https://github.com/mattpocock/skills) 改编，扩展了 common mistakes、when-to-deviate、退出码规范等内容。
