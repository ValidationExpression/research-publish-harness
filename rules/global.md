---
description: "Research Publish Agent 项目全局规则（架构不变量与专属约定）"
globs: "**/*"
alwaysApply: true
---

# Research Publish Agent — 项目全局规则

> 通用团队规范见 `01-global-base.mdc`、`02-frontend-frontend-web.mdc`、`03-python-python-backend.mdc`。

## 核心不变量（不可违背）

- 研究（Python / LangGraph）与发稿（Node / 浏览器 Cookie）**分离编排**，桌面端统一调度
- Cookie **不出本机**，经 Chrome 插件 → 本地 WebSocket 传输
- 报告必须**人工审阅**后才可发布；研究 Agent **不包含发布工具**
- 所有本地服务仅绑定 `127.0.0.1`
- 发稿默认 `draftOnly: true`，禁止无意改为直接发布

## 模块边界

| 包 | 职责 |
|---|---|
| `packages/desktop` | Electron 主/渲染进程、IPC 编排 |
| `packages/research-agent` | FastAPI + LangGraph 研究服务 |
| `packages/local-server` | 发稿 REST + WebSocket Cookie 桥 |
| `packages/core` | 平台适配器（不被 desktop 渲染进程直接引用） |
| `packages/cookie-provider` | Chrome 扩展，仅供给 Cookie |

## 跨模块调用

- 渲染进程只通过 `window.desktopApi`（preload）访问后端，**禁止**直接 `fetch` 本地服务
- 环境变量统一使用仓库根目录 `.env`，**禁止**在 `packages/research-agent/` 下再建 `.env` 副本
- 本地 API 契约以 `docs/contracts.md` 为准；变更须同步更新

## 验证要求

- TypeScript 变更后运行 `pnpm typecheck`
- 发稿链路变更考虑 `pnpm test:sync`
- core 工具函数变更运行 `pnpm --filter @wechatsync/core test`
