# ParseFlow - Intelligent PDF Table Extraction Tool

Convert complex image/table-based PDF files into structured JSON data.

## 🌟 Core Features

1.  **Structured PDF Document Extraction**
    *   Supports multi-page, long-form PDFs.
    *   Accurately extracts fields (Fields), tables (Tables), and checkboxes (Checkbox).
    *   Outputs clearly hierarchical JSON data.

2.  **Long-Image Chunking & Intelligent Merging (Advanced Chunking)**
    *   **Chunk Processing**: Splits each page into multiple overlapping chunks to handle dense tables and improve OCR accuracy.
    *   **Intelligent Merge**: Uses an LLM (Gemini Pro) to intelligently identify overlapping regions, automatically deduplicate, and keep the most complete data.
    *   **Order Preservation**: Strictly ensures the extracted results match the original top-to-bottom order of each module.

3.  **Automatic Fault Tolerance & Retry**
    *   Built-in JSON parsing retry mechanism that automatically fixes formatting errors when they occur.
    *   Automatically handles merging of tables that span across pages.

## 🛠️ Technical Implementation

1.  **Dual-Model Architecture**
    *   **Extract Layer (Extract)**: Uses `Google Gemini Flash` for fast, low-cost OCR recognition.
    *   **Logic Layer (Merge)**: Uses `Google Gemini Pro` to handle complex merge logic (Chunk Merge & Page Merge).

2.  **Prompt Engineering**
    *   **OCR**: Focuses on “what you see is what you get,” extracting only fully visible content.
    *   **Merge**: Leverages the LLM’s semantic understanding to identify duplicate content, replacing traditional rule-based code matching for better results.

## 🚀 Usage

```bash
# Default configuration (recommended): 2 chunks + intelligent merge
python pdf_table_extractor.py

# Custom number of chunks (3 chunks for ultra-dense documents)
python pdf_table_extractor.py --chunks 3


## 📂 input/output

*   `input/` PDF 
*   `output/` JSON 
