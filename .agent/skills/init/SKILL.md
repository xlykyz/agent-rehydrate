# Skill: init

项目状态目录初始化。确保 `.agent/_state/` 结构存在，并写下第一条日志。

---

## 职责

创建项目状态目录结构，写入模板文件，记录初始化日志。让后续 skill（log、wiki、rehydrate）可以在已知结构上运行。

---

## 模板文件

本 skill 的模板存放在 `.agent/skills/init/templates/` 目录下：

```
templates/
├── _schema.md                  ← 格式说明书
├── development-log.md          ← 日志文件（空壳）
└── wiki/
    └── _index.md               ← wiki 索引（空壳）
```

Agent 执行时直接复制这些文件到 `.agent/_state/`，**不要重新生成**。

---

## 执行流程

### 1. 初始化操作

依次执行：

1. 创建 `.agent/_state/logs/`、`.agent/_state/wiki/` 目录
2. 复制 `templates/_schema.md` → `.agent/_state/_schema.md`
3. 复制 `templates/development-log.md` → `.agent/_state/logs/development-log.md`
4. 复制 `templates/wiki/_index.md` → `.agent/_state/wiki/_index.md`

**规则：**
- 目录已存在 → 不动
- 文件已存在 → **不覆盖**
- 只复制缺失的文件

### 2. 建立初版 wiki

清空模板内容，扫描项目，输出初版 wiki：

1. 读取 `.agent/skills/init/templates/wiki/_framework.md`，了解 wiki 覆盖范围
2. 扫描项目根目录，阅读 README.md、配置文件、核心代码
3. 按框架主题逐项写入 `.agent/_state/wiki/` 下的文件
4. 更新 `_index.md`，注册所有新建文件

### 3. 写第一条日志

清空模板内容，写入第一条真实日志：

```
[YYYY-MM-DD HH:mm] init 初始化项目状态目录结构

创建 .agent/_state/logs/、.agent/_state/wiki/ 目录，写入模板文件。

结果：.agent/_state/ 结构初始化完成
```

### 4. 校验

确认以下文件/目录全部存在：

- [ ] `.agent/_state/_schema.md`
- [ ] `.agent/_state/logs/`
- [ ] `.agent/_state/logs/development-log.md`
- [ ] `.agent/_state/wiki/`
- [ ] `.agent/_state/wiki/_index.md`
- [ ] `.agent/skills/`
- [ ] `.agent/skills/rehydrate/SKILL.md`
- [ ] `.agent/skills/init/SKILL.md`
- [ ] `.agent/skills/log/SKILL.md`
- [ ] `.agent/skills/wiki/SKILL.md`

---

## gitignore 配置

确保 `.agent/skills/` 和 `.agent/_state/` 不被提交到版本控制：

1. `.gitignore` 不存在 → 创建，写入：
   ```
   .agent/skills/
   .agent/_state/
   ```
2. `.gitignore` 已存在 → 逐行检查，缺失的行追加到末尾

**注意**：只加这两行，不要改动 `.gitignore` 中已有的内容。

---

## 幂等性

本 skill 是幂等的。已初始化的项目再次执行不会产生任何副作用。

---

## 依赖

无。本 skill 是所有其他 skill 的前提。
