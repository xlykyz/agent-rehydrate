# Skill: wiki

管理 `state/wiki/` 中的项目知识沉淀。

---

## 职责

wiki 沉淀两类知识：1）项目本身（架构、模块、约定）；2）项目相关的领域知识。

---

## 文件结构

```
state/wiki/
├── _index.md              ← 目录索引（必须）
├── project-architecture.md
├── data-pipeline.md
└── ...
```

- `_index.md` 用表格列出所有主题

---

## 维护操作

### 新增

1. 创建 `.md` 文件
2. 写入内容
3. 更新 `_index.md` 追加条目

### 修改

1. 在变更处追加 `> **更新于 YYYY-MM-DD**：`
2. 保留旧内容

### 更正

1. 在错误内容下方追加 `> **更正 YYYY-MM-DD**：`
2. 不删原文

---

## 文件格式

```markdown
# 主题名称

> 一句话说明。

---

## 概述

核心内容。

## 详细说明

细节、规则、示例。
```

---

## _index.md 格式

```markdown
# Wiki 索引

| 主题 | 说明 |
|------|------|
| [项目概述](./project-architecture.md) | 技术栈、目录结构 |
```
