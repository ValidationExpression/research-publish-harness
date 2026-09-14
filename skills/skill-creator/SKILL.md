---
name: skill-creator
description: 当用户需要创建、修改或沉淀团队 Skill 时使用。典型触发："帮我做一个 skill""把这段通用逻辑沉淀成技能""优化现有 skill""Skill 应该放哪"。只用于 Cursor + team-harness 的落地约定，不要跑 Claude/Cowork 评测套件。
---

# Skill Creator（Cursor / team-harness）

把可复用流程写成 Skill，放进本仓库源目录，再生成到 `.cursor/skills/`。

## 何时该建

- 同一类任务会反复出现（接入配置中心、出 Spec、合规自检等）
- 步骤、路径、红线需要全队一致
- 不要为一次性任务建 Skill

先用 `find-skills` 确认没有现成轮子。

## 存放位置

| 目录 | 用途 |
|---|---|
| `skills/<name>/` | TeamAI 团队技能（本仓库） |
| `skills/common/<name>/` | team-harness 通用技能（旧体系） |

目录名即 Skill 名：小写 + 中划线。每个目录必须有 `SKILL.md`。

## SKILL.md 结构

```markdown
---
name: my-skill
description: 做什么，以及什么时候必须用。把触发场景写进 description，不要只写在正文。
---

# 标题

## 步骤
1. ...
2. ...

## 红线
- ...
```

- `description` 要同时写「做什么」和「何时触发」，写具体一点，避免欠触发。
- 长文档、脚本放到 `references/`、`scripts/`，不要全塞进 `SKILL.md`。

## 落地到 Cursor

1. 在 teamai harness 仓库写好 Skill。
2. 执行 `teamai push` 创建 PR，合并后全员 `teamai pull` 自动同步。
3. **新开 Agent 对话** 验证能否被触发。
