# Skill: rehydrate

进入项目后的入口 skill。恢复认知状态，决定下一步行动。

---

## 职责

判断项目状态，加载已有认知，让 Agent 进入可工作状态。

---

## 入口流程

### 1. 检查初始化状态

- `.agent/_state/` 不存在 → 执行 `init` skill 完成初始化
- `.agent/_state/logs/development-log.md` 不存在 → 执行 `init`
- `.agent/_state/wiki/_index.md` 不存在 → 执行 `init`

### 2. 加载已有认知

按以下顺序读取：

1. **`.agent/_state/wiki/_index.md`** — 了解项目有哪些知识沉淀
2. **按需读取 wiki 文件** — 恢复对项目的理解
3. **`.agent/_state/logs/development-log.md`** — 了解最近的执行历史

### 3. 进入工作状态

完成上述加载后，Agent 可以开始当前任务。

---

## 依赖

- 如果触发 init 流程，依赖 init 的所有子步骤
- 如果复用已有状态，依赖 wiki 目录和日志文件已存在
