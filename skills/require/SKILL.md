---
name: require
description: 一键生成 SwRS，自动串联所有环节从 CTS 输入到 SwRS 输出。Use this skill when the user asks to "生成 SwRS", "从 CTS 生成需求", "一键生成软件需求", "执行完整需求流程", mentions "SwRS 生成" or "需求标准化全流程".
---

# SwRS 一键生成

自动评估完备性，向用户推荐最优路径，用户选择后执行相应流程。

## 执行步骤

### Step 1：完备性评估（自动）

```
1. /cts-intake <CTS文件>
   → 输出：完备性等级（L3/L2/L1）+ 推荐路径 + 澄清清单
```

### Step 2：路径选择（用户选择或接受推荐）

根据完备性等级，向用户呈现推荐路径和备选方案，让用户选择：

**若判定为 L3 级别**（高质量输入）：
- 🚀 **推荐：快速路径**（3个步骤）
  ```
  2. /swrs-write <CTS文件> --level=L3 --mode=smart-convert
  3. /quality-gate artifacts/05_swrs.md --source=<CTS文件>
  ```
  
- 📋 **备选：完整路径**（6个步骤）
  ```
  2. /boundary-def <CTS文件> --matrix=<通信矩阵>
  3. /fc-extract <CTS文件> --boundary=artifacts/02_boundary.md
  4. /module-decomp artifacts/03_fc_list.md --boundary=artifacts/02_boundary.md
  5. /swrs-write artifacts/03_fc_list.md artifacts/04_module_decomp.md --boundary=artifacts/02_boundary.md
  6. /quality-gate artifacts/05_swrs.md --fc=artifacts/03_fc_list.md --boundary=artifacts/02_boundary.md
  ```

**若判定为 L2 级别**（部分信息）：
- 🚀 **推荐：平衡路径**（5个步骤）
  ```
  2. /boundary-def <CTS文件> --matrix=<通信矩阵>
  3. /fc-extract <CTS文件> --boundary=artifacts/02_boundary.md
  4. /swrs-write artifacts/03_fc_list.md --boundary=artifacts/02_boundary.md
  5. /quality-gate artifacts/05_swrs.md --fc=artifacts/03_fc_list.md --boundary=artifacts/02_boundary.md
  ```
  
- 📋 **备选：完整路径**（6个步骤）
  ```
  [执行所有6个步骤]
  ```

**若判定为 L1 级别**（基础信息）：
- 🚀 **推荐：完整路径**（6个步骤）
  ```
  [执行所有6个步骤]
  ```

## 执行选项

| 选项 | 说明 |
|------|------|
| `--path=fast` | 直接使用快速路径（跳过选择交互） |
| `--path=balanced` | 直接使用平衡路径 |
| `--path=full` | 直接使用完整路径 |
| `--skip-confirm` | 跳过确认，直接执行 |
| `--output=./` | 输出目录，默认 ./artifacts/ |

## 输出结构

```
artifacts/
├── 01_cts_intake.md          # CTS 准入报告 + 等级评分 + 路径推荐
├── 02_boundary.md            # 边界定义文档（如果执行）
├── 03_fc_list.md             # FC 功能清单（如果执行）
├── 04_module_decomp.md       # 模块分解结果（如果执行）
├── 05_swrs.md                # SwRS 软件需求
├── 06_quality_report.md      # 质量审查报告
└── swrs_final.md             # 最终交付物
```

## 执行示例

```bash
# 完整流程：自动评估，向用户呈现选择
/require ./CTS_泊车功能.docx

# 快捷用法：直接执行快速路径（仅L3有效）
/require ./CTS_泊车功能.docx --path=fast --skip-confirm

# 强制使用完整路径（无论等级如何）
/require ./CTS_泊车功能.docx --path=full --skip-confirm

# 指定输出目录
/require ./CTS_泊车功能.docx --output=./泊车项目/
```
