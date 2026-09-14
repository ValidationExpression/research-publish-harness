---
name: find-skills
description: 当用户需要查找是否已有可复用的 Skill（团队内部的或社区的）、或想知道"这个功能有没有现成技能"时使用。典型触发："有没有处理 XX 的 skill""找个能 XX 的技能""这个功能要自己写还是用现成的""先看看有没有轮子"。
---

# Skill 搜索器

本 Skill 指导你在动手前先找"已有的轮子"，避免重复造 Skill（团队红线：复用优先）。

## 查找顺序
1. **团队 Skills（优先）**：查看 team-harness 的 `skills/common/` 与 `skills/business/`；已同步到业务项目 `.cursor/skills/` 的也可直接调用。
2. **Cursor / 社区 Skills**：查看 `~/.cursor/skills/`、Cursor 官方与社区 Skill；不要与本仓库 `skills/` 源目录混淆。
3. **判断复用策略**：
 - 已有 Skill 覆盖约 80% 需求 → 直接复用，必要时让 AI 微调用法
 - 部分覆盖 → 复用现有 + 在本项目补充 `references/`
 - 完全不覆盖 → 用 `skill-creator` 新建，并放进正确目录

## 决策原则
- 复用优先于新建。
- 新 Skill 必须放进正确目录（`common/`=通用，`business/`=业务），否则 sync 不会下发。
- 不为一次性任务创建 Skill。
- 找到候选 Skill 后，向用户说明"已有 X 可复用，是否直接用它"，而非默默重写。
