---
name: require
description: 一键生成 SwRS，自动串联所有环节从 CTS 输入到 SwRS 输出。Use this skill when the user asks to "生成 SwRS", "从 CTS 生成需求", "一键生成软件需求", "执行完整需求流程", mentions "SwRS 生成" or "需求标准化全流程".
---

# SwRS 一键生成

自动串联全流程：cts-intake → boundary-def → fc-extract → module-decomp → swrs-write → quality-gate

## 输入依赖

- **必须**：CTS 文档
- **可选**：通信矩阵（--matrix）

## 执行流程

```
1. /cts-intake <CTS文件>
   → 保存到 artifacts/01_cts_intake.md

2. /boundary-def <CTS文件> --matrix=<通信矩阵>
   → 保存到 artifacts/02_boundary.md

3. /fc-extract <CTS文件> --boundary=artifacts/02_boundary.md
   → 保存到 artifacts/03_fc_list.md

4. /module-decomp artifacts/03_fc_list.md --boundary=artifacts/02_boundary.md
   → 保存到 artifacts/04_module_decomp.md

5. /swrs-write artifacts/03_fc_list.md artifacts/04_module_decomp.md --boundary=artifacts/02_boundary.md
   → 保存到 artifacts/05_swrs.md

6. /quality-gate artifacts/05_swrs.md --fc=artifacts/03_fc_list.md --boundary=artifacts/02_boundary.md
   → 保存到 artifacts/06_quality_report.md
```

## 执行选项

| 选项 | 说明 |
|------|------|
| `--phase=N` | 执行到 Phase N 后停止（1-5） |
| `--skip-review` | 跳过质量网关审查 |
| `--output=./` | 输出目录，默认 ./artifacts/ |

## 输出结构

```
artifacts/
├── 01_cts_intake.md      # CTS 准入报告
├── 02_boundary.md        # 边界定义文档
├── 03_fc_list.md         # FC 功能清单
├── 04_module_decomp.md   # 模块分解结果
├── 05_swrs.md            # SwRS 软件需求
├── 06_quality_report.md  # 质量审查报告
└── swrs_final.md         # 最终交付物
```

## 执行示例

```bash
# 完整流程
/require ./CTS_泊车功能.docx

# 只执行到 Phase 3
/require ./CTS_泊车功能.docx --phase=3

# 跳过质量审查
/require ./CTS_泊车功能.docx --skip-review

# 指定输出目录
/require ./CTS_泊车功能.docx --output=./泊车项目/
```
