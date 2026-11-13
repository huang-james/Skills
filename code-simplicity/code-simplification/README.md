# code-simplification · 代码简化

> 在**行为完全不变**的前提下简化代码。目标不是更少的行数，而是更容易读、更容易懂、
> 更容易改、更容易调试的代码。检验标准只有一条：**新人理解简化版是否比原版更快？**

灵感来自 [Claude Code Simplifier plugin](https://github.com/anthropics/claude-plugins-official/blob/main/plugins/code-simplifier/agents/code-simplifier.md)，改写为模型无关、流程驱动的通用技能。

## 适用场景

- 功能已跑通、测试已通过，但实现"感觉偏重"
- Code review 中被标记可读性或复杂度问题
- 遇到深层嵌套、超长函数、命名不清
- 整理时间压力下写出的代码
- 合并代码后出现重复或不一致

**不适用**：代码已经很干净（别为简化而简化）；还没读懂代码在做什么；性能敏感且"简化版"确实更慢；模块本来就要整体重写。

## 五大原则

1. **行为完全不变** —— 输入输出、副作用、错误行为、边界情况必须一模一样；不确定是否等价，就不改。
2. **遵循项目约定** —— 简化是向代码库风格靠拢，不是强加个人偏好；破坏一致性的"简化"是搅动。
3. **清晰优先于炫技** —— 需要停下来才能解析的紧凑写法，不如显式的直白写法（如嵌套三元 → if/else）。
4. **保持平衡** —— 警惕过度简化：别内联掉有名字的辅助函数、别合并无关逻辑、别删可扩展性抽象、别为行数优化。
5. **只动改过的代码** —— 默认只简化最近修改的代码，不顺手重构无关模块。

## 四步流程

1. **动手前先理解**（Chesterton's Fence）：这段代码的职责、调用关系、边界情况、存在原因——答不上来就先别动
2. **识别简化机会**：按结构复杂度（深层嵌套/长函数/嵌套三元）、命名（泛型名/误导名）、冗余（重复逻辑/死代码/过度抽象）三类信号扫描
3. **增量应用**：一次一个简化，每次跑测试；重构改动与功能修复**分开提交**；超过 500 行的重构用自动化工具而非手改
4. **验证结果**：简化版真的更易懂吗？diff 干净可审吗？队友会批准吗？——若不然，回滚

## 语言速查示例

```typescript
// 之前：多余的 async 包装 + 冗长条件赋值
async function getUser(id: string): Promise<User> {
  return await userService.findById(id);
}
// 之后
function getUser(id: string): Promise<User> {
  return userService.findById(id);
}
const displayName = user.nickname || user.fullName;
```

```python
# 之前：嵌套条件层层包裹
def process(data):
    if data is not None:
        if data.is_valid():
            ...
# 之后：卫语句提前返回
def process(data):
    if data is None:
        raise TypeError("Data is None")
    ...
```

## 危险信号

- 简化后需要改测试才能通过（大概率改了行为）
- "简化"后的代码更长更难读
- 按个人喜好而非项目约定重命名
- 以"让代码更干净"为由删除错误处理
- 大量简化堆进一个难以审查的提交

## 使用方式

安装后由智能体在简化/重构/清理代码时调用，或手动 `/code-simplification` 触发。

## 安装

```bash
# ZCode
cp -r code-simplicity/code-simplification ~/.zcode/skills/

# Claude Code
cp -r code-simplicity/code-simplification ~/.claude/skills/
```
