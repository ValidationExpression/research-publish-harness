# research-publish-harness

TeamAI 团队 Harness 仓库，为 [research-publish-agent](https://github.com/ValidationExpression/research-publish-agent) 提供统一的 AI 协作资产：

- **skills** — 可复用技能
- **rules** — 编码规范（全局 / 前端 / Python）
- **docs** — 项目文档与约定
- **learnings** — 团队经验沉淀（随使用积累）

## 关联项目

| 仓库 | 用途 |
|------|------|
| [research-publish-agent](https://github.com/ValidationExpression/research-publish-agent) | 业务应用（Electron + LangGraph + 多平台发稿） |
| [team-harness](https://github.com/ValidationExpression/team-harness) | 旧版 Harness 源（本仓库规则从此迁移） |

## 成员使用

```bash
cd /path/to/research-publish-agent
teamai init https://github.com/ValidationExpression/research-publish-harness --agent cursor
teamai pull
```

每次打开 Cursor 会话时会通过 hooks 自动 `pull` 最新资源。

## 贡献

```bash
# 在本地 AI 工具中新增/修改 skill 或 rule 后
teamai push
```

会创建 PR，审核合并后全员自动同步。
