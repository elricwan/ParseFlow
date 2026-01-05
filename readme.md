# ParseFlow - PDF 表格智能提取工具

将复杂的图片/表格 PDF 文件转化为结构化的 JSON 数据。

## 🌟 核心功能

1.  **PDF 文档结构化提取**
    *   支持多页、长表单 PDF。
    *   精准提取字段 (Fields)、表格 (Tables)、勾选框 (Checkbox)。
    *   输出层级分明的 JSON 数据。

2.  **长图分块与智能合并 (Advanced Chunking)**
    *   **分块处理**：将页面切分为多个重叠的分块，以应对密集表格，提高 OCR 精度。
    *   **智能合并**：使用 LLM (Gemini Pro) 智能识别重叠区域，自动去重并保留最完整数据。
    *   **顺序保持**：严格保证提取结果与原文各个模块的上下顺序一致。

3.  **自动容错与重试**
    *   内置 JSON 解析重试机制，遇到格式错误自动修正。
    *   自动处理跨页表格的合并。

## 🛠️ 技术实现

1.  **双模型架构**
    *   **提取层 (Extract)**: 使用 `Google Gemini Flash` 进行快速、低成本的 OCR 识别。
    *   **逻辑层 (Merge)**: 使用 `Google Gemini Pro` 处理复杂的合并逻辑（Chunk Merge & Page Merge）。

2.  **Prompt Engineering**
    *   **OCR**：专注于“所见即所得”，只提取完整可见内容。
    *   **Merge**：利用 LLM 的语义理解能力来判断重复内容，代替传统的代码规则匹配，效果更优。

## 🚀 使用方法

```bash
# 默认配置（推荐）：2分块 + 智能合并
python pdf_table_extractor.py

# 自定义分块数量（3块用于超密集文档）
python pdf_table_extractor.py --chunks 3
```

## 📂 输入输出

*   输入：`input/` 文件夹下的 PDF 文件
*   输出：`output/` 文件夹下的 JSON 文件