# Agent Rehydrate

> **项目级状态重建协议** — 让任何 AI Agent 进入项目时，都能快速恢复一致的认知状态。
>
> 🚀 **快速启动：** 无需从零创建 AGENT.md，`protocol/AGENT.md` 复制到新项目根目录即可，复制即用。
>
> 💾 **长期记忆：** 构建 agent 专属长期项目记忆，沉淀到本地文件，开箱即可理解整个项目。

---

## 一句话定义

这是一个用于降低 AI 编程 Agent 在项目中 **"状态重建成本"（State Rehydration Cost）** 的项目级协议系统。

它不是 Agent 系统，不是 prompt 工程，而是——让任何强 Agent 进入项目时，快速恢复一致认知与工作状态的**协议层**。

---

## 核心痛点

AI 在**单次任务执行**上是强的，但在**跨任务、跨时间的一致性**上是弱的。

每一次调用 Agent，它都像是一个"刚进入项目的新开发者"，需要重新建立对项目的整体理解。这种不断"重新解释世界"的过程，构成了长期开发中最大的隐性成本——**状态重建成本**。

本项目正是针对这一问题提出的结构化解决方案。

---

## 系统架构

### 核心闭环

每个 Agent 只做三件事：

```
1. Rehydrate（恢复状态）
   → 读取 AGENT.md（协议）
   → 读取 state/（事实）
   → 建立一致认知

2. Execute（执行任务）
   → 完成当前任务

3. Persist（写回状态）
   → 更新 logs（发生了什么）
   → 更新 tasks（状态变化）
   → 更新 memory（稳定事实）
   → 更新 wiki（结构化知识）
```

---

## 项目结构

```
project-root/
├── AGENT.md           # 行为规则与状态访问协议
├── README.md          # 项目说明

└── state/             # 唯一事实来源
    ├── _schema.md     # 状态目录结构与格式规范
    ├── docs/          # 架构决策与设计文档
    ├── logs/          # 执行历史（发生了什么）
    ├── tasks/         # 当前工作状态（TODO / in-progress / done）
    ├── memory/        # 稳定、经过验证的事实性知识
    └── wiki/          # 结构化领域知识
```

---

## 设计原则

| 传统 Agent | 本协议系统 |
|---|---|
| 状态归属人脑 | 状态归属 repo |
| 生命周期 = 单次任务 | 生命周期 = 长期项目 |
| 上下文临时生成 | 上下文可恢复 |
| 行为模式 = 执行指令 | 行为模式 = 状态演化 |
| 文档作用弱 | 文档是核心组成 |
| 适用 feature 级修改 | 适用项目级开发 |

---

## 使用方式

### 新项目

```bash
# 将 protocol 复制到新项目
cp -r agent-rehydrate/protocol/AGENT.md my-new-project/
mkdir -p my-new-project/state/{docs,logs,tasks,memory,wiki}
```

### 已有项目

```bash
# 引入状态层
mkdir -p project/state/{docs,logs,tasks,memory,wiki}
cp agent-rehydrate/protocol/AGENT.md project/
```

---

## 项目定位

本项目不是 AI 框架，不是自动化系统，也不是 prompt 集合。

它的本质是一个**协议层设计**——定义的是"用于约束 AI Coding Agent 行为一致性的项目级状态协议"。

它不试图改变 AI 的能力，而是改变 AI 进入项目时的**方式**。

---

## LICENSE

MIT
