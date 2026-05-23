# Agent Rehydrate — AGENT.md

> 本仓库是 Agent Rehydrate 协议本身的实现。
> AGENT.md 是可复用的协议模板，存放于 `protocol/AGENT.md`。
> 本文件描述本项目自身的操作规则。

---

## 0. 目录结构

```
agent-rehydrate/
├── AGENT.md              ← 本文档（本项目的操作规则）
├── README.md             ← 设计宣言/项目说明
│
├── protocol/
│   └── AGENT.md          ← 核心产物：可复用于任何项目的协议模板
│
├── state/                ← 状态层（本项目的演化记录）
│   ├── _schema.md        ← 状态目录格式规范
│   ├── logs/
│   ├── tasks/
│   ├── memory/
│   └── wiki/
│
└── docs/
    ├── audits/           ← 审计报告归档
    ├── decisions.md
    └── architecture.md
```

---

## 1. 核心工作流

### 读取顺序（Rehydration）

```
1. state/tasks/status.md    → 当前进度
2. state/memory/            → 稳定事实
3. docs/                    → 架构决策
```

### 写回规则（Persist）

每次修改后：
- 更新 `state/logs/development-log.md`
- 更新 `state/tasks/status.md`
- 更新 `state/memory/` — 仅稳定事实，至少 2 次验证

---

## 2. 本仓库的维护职责

### protocol/AGENT.md 的迭代

- 这是本仓库的核心产物
- 协议版本变更必须记录在 `docs/decisions.md`
- 每次发布新版本前，运行以下验证：
  - 与 `state/_schema.md` 定义的格式一致
  - 涵盖全部 9 节内容
  - 无内部矛盾

### 变更流程

1. 读 `state/tasks/status.md` 找待办
2. 读 `state/memory/` 回顾上下文
3. 执行修改
4. 更新 `state/tasks/status.md`
5. 更新 `state/logs/development-log.md`
6. 更新 `state/memory/`（如适用）
