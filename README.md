# Agent Rehydrate

> **项目级状态重建协议 v2.0** — 让 AI Agent 进入项目时，快速恢复一致的认知状态。
>
> 🚀 **快速启动：** 复制 `protocol/AGENTS.md` 到新项目根目录，首次进入时 Agent 自动拉取 skill 体系，开箱即用。
>
> 💾 **长期记忆：** 通过 logs（执行历史）+ wiki（结构化知识）沉淀项目认知，Agent 每次进入都能恢复上下文。

---

## 核心哲学

本项目是**状态驱动**的。仓库（repo）是唯一可信的现实来源，所有认知从文件结构中恢复，不依赖模型的隐式记忆。

**一致性不依赖"智能"，而依赖结构。**

---

## 系统架构

### 协议 + Skill 体系

AGENTS.md 是协议本体（~150 行），定义行为契约。操作细节封装在独立 skill 中，不嵌入协议文件。

```
AGENTS.md（协议本体）
  │
  ├── 技能引导（首次自动克隆 .agent/skills/）
  ├── 入口流程（rehydrate → init / 开工）
  ├── 运行时约定（何时调 log / wiki）
  └── 一致性约束
               
.agent/skills/（操作定义）
  ├── rehydrate/  ← 入口：检查初始化 → 加载认知 → 分流
  ├── init/       ← 建目录 → 复制模板 → 建初版 wiki → 写日志
  ├── log/        ← 向 development-log.md 追加执行记录
  └── wiki/       ← 维护 .agent/_state/wiki/ 中的项目知识
```

### 工作流程

```
Agent 进入项目
     │
     ├── .agent/skills/ 不存在？→ 从 GitHub 自动克隆
     │
     ▼
  加载 rehydrate skill
     │
     ├── 未初始化 → init（建 .agent/_state/ + 写 wiki + 日志）
     │
     └── 已初始化 → 加载 wiki + logs → 恢复认知
                           │
                           ▼
                         开工
                           │
                           ├── 有知识沉淀？→ wiki skill
                           │
                           └── 总是 → log skill（追加记录）
```

---

## 项目结构

```
project-root/
├── AGENTS.md           # 协议本体（复制即用）
├── README.md
├── skills/             # 技能源码（分发源）
│   ├── rehydrate/
│   ├── init/
│   ├── log/
│   └── wiki/
├── docs/               # 开发文档与审计
└── protocol/
    └── AGENTS.md       # 协议模板
```

---

## v2.0 相比 v1.x 的变化

| 维度 | v1.x | v2.0 |
|------|------|------|
| 协议本体 | 211 行，内嵌所有操作细节 | ~150 行，只留契约 + skill 引用 |
| 操作逻辑 | 写在 AGENTS.md 里 | 封装为独立 skill |
| state 结构 | logs / tasks / memory / wiki | logs + wiki（仅客观层） |
| 入口流程 | 直接开始执行 | rehydrate 检查 → 分流 |
| 使用方式 | 复制一个文件 | 复制 AGENTS.md → 自动拉 .agent/skills/ |

---

## 使用方式

复制 `protocol/AGENTS.md` 到新项目根目录即可：

```bash
cp agent-rehydrate/protocol/AGENTS.md my-project/AGENTS.md
```

AI 工具对应的文件名：

| 工具 | 文件名 |
|------|--------|
| Claude | `CLAUDE.md` |
| Codex / OpenCode | `AGENTS.md` |
| Cursor | `.cursor/rules/core.mdc` |
| Trae | `user_rules.md`（全局规则）或设置 → 规则 |

首次进入时，Agent 会自动检测 `.agent/skills/` 是否存在：
- **有网** → 自动从 `github.com/xlykyz/agent-rehydrate` 克隆
- **无网** → 显示提示信息，手动复制 `.agent/skills/` 目录即可

---

## 设计原则

| 传统 Agent | 本协议系统 |
|---|---|
| 状态归属人脑 | 状态归属 repo |
| 生命周期 = 单次任务 | 生命周期 = 长期项目 |
| 上下文临时生成 | 上下文可恢复 |
| 行为模式 = 执行指令 | 行为模式 = 状态演化 |
| 文档作用弱 | 文档是核心组成 |

---

## 项目定位

本项目不是 AI 框架，不是自动化系统，也不是 prompt 集合。

它的本质是一个**协议层设计**——定义的是"用于约束 AI Coding Agent 行为一致性的项目级状态协议"。它不试图改变 AI 的能力，而是改变 AI 进入项目时的**方式**。

---

## LICENSE

MIT
