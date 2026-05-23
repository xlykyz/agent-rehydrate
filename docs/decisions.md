# Architecture Decisions

> Architecture Decision Records (ADR) for Agent Rehydrate.

## ADR-001: 状态层使用 /state/ 前缀

- **日期**: 2026-05-23
- **状态**: Accepted
- **背景**: AGENTS-v1.0 初版将 logs/tasks/memory/wiki/docs 放在根目录，而设计 spec 使用 /state/ 前缀。审计报告指出不一致。
- **决策**: 统一使用 /state/ 前缀。根目录的 /docs 保留为工作层文档。
- **理由**: 符合"状态层"的命名空间隔离设计，避免根目录污染。
- **影响**: 所有引用状态文件的路径需更新为 /state/ 开头。

## ADR-002: docs 移至项目根目录

- **日期**: 2026-05-23（2026-05-19 更新）
- **状态**: Accepted
- **背景**: 原设计将 docs 归入 /state/，审计发现 state/docs 与根目录 /docs 存在命名冲突。后续重构确定 state 只存放 Agent 认知状态，docs 属项目文档而非 Agent 状态。
- **决策**: 撤销 ADR-002 原决案。docs 移至项目根目录，不作为 state 子目录。state 缩减为 logs/ + wiki/（MVP 阶段）。
- **理由**: docs 是面向人的项目文档，不属于 Agent 状态系统。state 聚焦 Agent 认知状态，职责更清晰。
- **影响**: protocol/AGENTS.md 已更新移除 state/docs 引用。project-root/docs/ 作为独立目录存在。

## ADR-003: tasks 使用单文件 status.md

- **日期**: 2026-05-23
- **状态**: Accepted
- **背景**: 审计报告指出 tasks 目录未定义文件格式。
- **决策**: 使用单个 status.md 文件管理所有任务状态，GFM 任务列表标记。
- **理由**: 单文件降低 Agent 读写复杂度，减少"到底读哪个文件"的歧义。
