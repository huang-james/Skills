# code-simplicity · 代码简洁性组合

> 两个配套的简洁性技能：一个管**写之前**，一个管**写完之后**。配合使用，让代码始终保持在人类一遍能读懂的范围内。

## 组合关系

```
写代码前  →  simplicity-first      （门槛：先找最小方案，过度复杂 = bug）
写完之后  →  code-simplification   （清理：行为不变地简化已有代码）
```

| | [simplicity-first](./simplicity-first/README.md) | [code-simplification](./code-simplification/README.md) |
|---|---|---|
| **角色** | 预防性门槛 | 补救性重构 |
| **触发时机** | 编写/修改任何代码**之前**；审查 diff 之前 | 代码能跑但难读、难维护时；review 标记复杂度问题时 |
| **核心主张** | 过度复杂、体量过大 = 正确性 bug | 行为完全不变的前提下降低复杂度 |
| **关键产出** | 更小的 diff、更少的概念 | 更易懂的实现、干净的 diff |

## 为什么放在一起

两者是同一原则的两个执行面：**简洁是核心工程指标，不是风格偏好**。前者阻止复杂度进场，后者清退已进场的复杂度——单独装一个都只覆盖半程。

## 安装

```bash
# ZCode
cp -r code-simplicity/simplicity-first ~/.zcode/skills/
cp -r code-simplicity/code-simplification ~/.zcode/skills/

# Claude Code
cp -r code-simplicity/simplicity-first ~/.claude/skills/
cp -r code-simplicity/code-simplification ~/.claude/skills/
```
