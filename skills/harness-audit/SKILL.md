---
name: "harness-audit"
description: "团队 Harness 规范自动化合规自检。当需要评估一个项目是否按《Harness Engineering 落地规范》配置 Rules/Skills/MCP/AGENTS.md/Plan 模式/工程规范/Commit 规范时使用：对项目打分、诊断问题、给出 P0~P3 改进建议。触发场景：(1) 项目初次接入规范 (2) 提交 PR 前自查 (3) 季度团队复盘 (4) 新项目立项 2 周内检查"
---
# harness-audit 合规自检 Skill

把整套团队规范的检查项固化成一个可执行的合规性审计工具。一句话给项目打分、找问题、给建议。

## 审计维度与权重（对应规范章节）
| 维度 | 权重 | 对应章节 |
| --- | --- | --- |
| 1. AGENTS.md（AI 说明书） | 15% | §4.4 |
| 2. Rules（约束体系） | 20% | §4.3 |
| 3. Skills（技能沉淀） | 15% | §5.4 |
| 4. MCP（上下文扩展） | 10% | §5.1 |
| 5. Plan 模式（SDD） | 15% | §5.5 |
| 6. 项目工程规范 | 15% | §6 |
| 7. Commit 规范与协作 | 10% | §6.2 / §7 |

总分 100，按 S/A/B/C/D 五级评定。

## 执行方式
本 Skill 附带 `audit.py` 脚本，自动完成"信息采集 → 逐维度评分 → 生成报告"三阶段：

```bash
# 审计当前目录项目
python3 skills/harness-audit/audit.py .

# 指定输出目录（生成报告保持本地，不要提交）
python3 skills/harness-audit/audit.py /path/to/project --out .tmp-harness-audit
```

脚本会检查 `AGENTS.md` 是否包含模板章节（接受「项目简介」等实际标题，不要求必须写成「项目概述」），并在 Cursor / Codex / Claude Code / CodeBuddy / OpenCode / MiMo Code / Qoder 的落地目录中查找 Rules、Skills、MCP 与 Plan。

报告默认写入 `.cursor/reports/harness-audit-{项目名}-{日期}.md`；使用 `--out .tmp-harness-audit` 时写入该目录。在对话中展示摘要。

## 评分后动作
- 🔴 P0：立即修复（如未接入 DB MCP、Commit 格式混乱）
- 🟠 P1：短期改进（统一 Commit 规范、建立 Plan 归档）
- 🟡 P2 / 🔵 P3：持续优化

> ⚠️ 审计报告是体检结果，不是 KPI。重点是发现问题、推动改进，不要为了刷分而刷分。
