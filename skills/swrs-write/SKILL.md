---
name: swrs-write
description: SwRS 软件需求编写，为每个模块推导软件需求并遵循 ISO 26262。Use this skill when the user asks to "编写 SwRS", "生成软件需求规格", "写软件需求文档", "SwRS 文档生成", mentions "SwRS writing" or discusses 软件需求规格编写.
---

# SwRS 编写

## 输入依赖

- **必须**：FC 功能清单
- **必须**：模块分解结果
- **必须**：边界定义文档（--boundary，包含接口定义）

## 推导规则

1. SMART 原则：Specific, Measurable, Achievable, Relevant, Testable
2. 所有数值参数必须量化，不允许模糊词
3. 每条 SwSR 需说明可验证方式
4. 必须包括：输入、输出、功能逻辑

## SwSR 卡片模板

```markdown
需求ID: SwSR-[模块]-[功能]-[编号]
功能名称: [简洁功能名]
触发条件: [精确描述触发该功能的事件或状态]
输入: [(信号名, 数据类型, 取值范围/枚举)]
预期行为: [量化描述，如"在 X ms 内完成 Y"]
输出: [(信号名, 数据类型, 输出值/范围)]
例外处理: [异常输入或边界条件下的行为]
源FC: [对应的 FC-ID]
```

## 量化检查

| 模糊描述 | 量化要求 |
|---------|----------|
| "低速" | "< 30 km/h" |
| "快速响应" | "响应时间 ≤ 100 ms" |
| "合理范围" | "[最小值, 最大值]" |

## ID 命名示例

- `SwSR-MFF-HMISwitch-01`
- `SwSR-MFF-conf-01`
- `SwSR-MFF-UNP-01`

## 执行示例

```bash
/swrs-write ./FC清单.md ./模块分解.md --boundary=./边界定义.md
```
