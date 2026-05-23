# AGENTS.md v2.0

> 项目级状态重建协议
>
> 本文档是 AI Agent 进入此项目时的行为契约。
> 它不是 prompt 集合，而是行为与状态的协议。

---

## 核心概念

本项目是**状态驱动**的。仓库（repo）是唯一可信的现实来源，所有认知从文件结构中恢复，不依赖模型的隐式记忆。

```
state/
├── logs/     ← 执行历史（客观、不可变）
└── wiki/     ← 项目认知（结构化、稳定）
```

---

## 角色定义

你是此项目的**执行 Agent**。职责：

- 基于 skill 执行标准操作
- 维护项目状态一致性
- 持续沉淀项目知识

---

## Skill 体系

所有操作由以下 skill 定义：

| Skill | 职责 | 路径 |
|-------|------|------|
| rehydrate | 入口：检查初始化 → 加载认知 → 分流 | `skills/rehydrate/SKILL.md` |
| init | 创建目录 → 复制模板 → 建初版 wiki → 写日志 | `skills/init/SKILL.md` |
| log | 向 development-log.md 追加执行记录 | `skills/log/SKILL.md` |
| wiki | 维护 state/wiki/ 中的项目知识 | `skills/wiki/SKILL.md` |

---

## 首次使用：技能引导

如果项目根目录下 `skills/` **不存在**，说明此项目尚未具备技能体系。按以下步骤加载：

1. **从仓库拉取技能**：`git clone --depth 1 https://github.com/xlykyz/agent-rehydrate.git .agent-tmp && cp -r .agent-tmp/skills/ ./ && rm -rf .agent-tmp`
2. **验证结果**：确认 `skills/` 存在且包含四个 skill 目录
3. **拉取失败**（网络不通等）：输出以下提示并停止

> **⚠️ Skill 加载失败**
> 本协议需要 skill 体系才能运作。请手动将以下仓库中的 `skills/` 目录复制到项目根目录：
> `https://github.com/xlykyz/agent-rehydrate`

完成后，继续按入口流程执行。

---

## 入口流程

```
1. 加载 rehydrate skill
2. 按 rehydrate 判断：未初始化 → 调 init；已初始化 → 加载 wiki + logs
3. 开工
4. 按"运行时约定"更新状态
```

---

## 运行时约定

以下规则**整个会话期间**有效，每次执行操作后必须遵守。

### 调用 log skill

**每次**完成一个有意义的具体操作后调用 log skill 追加记录。例如：

- 创建/修改/删除文件后
- 数据拉取或处理后
- 配置变更后
- 做出决策后

只写"已完成的事"，不写"正在做的事"。

### 调用 wiki skill

当以下条件**全部满足**时调用 wiki skill 新增或更新知识：

- 信息是稳定、已验证的（非假设、非单次观察）
- 对后续工作有复用价值
- 已有 wiki 中未覆盖此内容

不需要每次操作都写 wiki，只在有知识沉淀时才写。

### 执行顺序

```
修改操作完成
     │
     ├── 有知识沉淀需求？ → 调用 wiki skill
     │
     └── 总是 → 调用 log skill（追加执行记录）
```

---

## 一致性约束

- logs 只追加，不修改
- wiki 只写入已验证、可复用的结构化知识
- 每次操作后更新 logs
- 未初始化不得执行修改操作

---

## 系统哲学

一致性不依赖"智能"，而依赖结构。
