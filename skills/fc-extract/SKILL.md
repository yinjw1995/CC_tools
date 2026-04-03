---
name: fc-extract
description: FC 功能提取，从 CTS 提取独立功能点并生成 FC 需求卡片。Use this skill when the user asks to "提取功能需求", "生成 FC 清单", "功能需求提取", "从 CTS 提取 FC", mentions "FC extraction" or discusses 功能需求分析.
---

# FC 功能提取

## 输入依赖

- **必须**：CTS 文档（经边界定义后）
- **必须**：边界定义文档（--boundary）

## 处理规则

1. 识别所有独立的功能需求，每个功能对应一张卡片
2. 若文档中无编号，顺序分配 FC-001, FC-002...
3. 分别提取功能需求和非功能需求

## FC 卡片模板

```markdown
需求ID: FC-XXX
功能名称: [简洁功能名]
源文档位置: [原文引用片段]
```

卡片间用 `---` 分隔。

## 非功能需求汇总

| 维度 | 描述 | 指标 |
|------|------|------|
| 性能 | | |
| 安全 | | |
| 可靠性 | | |
| 合规 | | |

## 执行示例

```bash
/fc-extract ./CTS_泊车功能.docx --boundary=./边界定义.md
```
