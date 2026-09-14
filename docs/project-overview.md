# Research Publish Agent — 项目概览

> 业务仓库：https://github.com/ValidationExpression/research-publish-agent

## 业务用途

AI 深度研究 + 人工审阅 + 多平台草稿发布桌面应用。

## 核心不变量

- 研究（Python / LangGraph）与发稿（Node / 浏览器 Cookie）分离编排
- Cookie 不出本机
- 报告必须人工审阅后才可发布
- 所有本地服务仅绑定 `127.0.0.1`
- 发稿默认 `draftOnly: true`

## 技术栈

| 模块 | 路径 | 技术 |
|------|------|------|
| 桌面端 | `packages/desktop` | Electron + React |
| 研究服务 | `packages/research-agent` | Python FastAPI + LangGraph |
| 发稿服务 | `packages/local-server` | Node HTTP + WebSocket |
| 平台适配 | `packages/core` | TypeScript 适配器 |
| Cookie 插件 | `packages/cookie-provider` | Chrome Extension |

## 常用命令

```bash
pnpm desktop:dev      # 启动桌面端（推荐）
pnpm typecheck        # TypeScript 类型检查
pnpm test:sync        # 发稿 E2E 测试
```

环境变量统一使用仓库根目录 `.env`（从 `.env.example` 复制）。
