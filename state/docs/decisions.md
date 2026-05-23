# Architecture Decisions

> Architecture Decision Records (ADR) for Agent Rehydrate.

## ADR-001: 状态层使用 /state/ 前缀

- **日期**: 2026-05-23
- **状态**: Accepted
- **背景**: AGENT-v1.0 初版将 logs/tasks/memory/wiki/docs 放在根目录，而设计 spec 使用 /state/ 前缀。审计报告指出不一致。
- **决策**: 统一使用 /state/ 前缀。根目录的 /docs 保留为工作层文档。
- **理由**: 符合"状态层"的命名空间隔离设计，避免根目录污染。
- **影响**: 所有引用状态文件的路径需更新为 /state/ 开头。

## ADR-002: docs 归入 /state/ 统一管理

- **日期**: 2026-05-23
- **状态**: Accepted（2026-05-23 更新）
- **背景**: 原 spec 4.2 包含 /state/docs，4.3 又定义 /docs 为工作层，构成命名冲突。审计报告指出此问题。
- **决策**: 所有状态文件统一放在 /state/ 下，docs 归入 state/docs/。不再分"状态层 docs"和"工作层 docs"。
- **理由**: 消除命名冲突，简化结构，用户反馈三层架构过于复杂。
- **影响**: 所有引用 docs 的路径改为 state/docs/。

## ADR-003: tasks 使用单文件 status.md

- **日期**: 2026-05-23
- **状态**: Accepted
- **背景**: 审计报告指出 tasks 目录未定义文件格式。
- **决策**: 使用单个 status.md 文件管理所有任务状态，GFM 任务列表标记。
- **理由**: 单文件降低 Agent 读写复杂度，减少"到底读哪个文件"的歧义。
