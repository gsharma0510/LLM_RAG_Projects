# Project 01: Local RAG Demo (Financial Analysis) 📈

This project demonstrates a **Retrieval-Augmented Generation (RAG)** pipeline running entirely on local hardware. It uses a 2025 Alphabet (Google) 10-K report to provide context-aware answers to financial and risk-related questions.

## 🛠️ Tech Stack
* **PDF Extraction:** `pypdf`
* **Embeddings:** `all-MiniLM-L6-v2` (Sentence-Transformers)
* **Vector Database:** `FAISS` (Facebook AI Similarity Search)
* **LLM Engine:** `Ollama` running `Llama 3.2 1B`

## 📂 Data Source
* **File:** `alphabet_10k_2025.pdf`
* **Description:** The Annual Report for Alphabet Inc. for the fiscal year ended December 31, 2025.

## 🚀 How to Run
1. **Prepare Ollama:**
   - Ensure Ollama is installed.
   - Run `ollama pull llama3.2:1b` in your terminal.
2. **Setup Notebook:**
   - Open `Local_RAG_Notebook.ipynb`.
   - Ensure your `.conda` environment is active and the `alphabet_10k_2025.pdf` is in the same folder.
3. **Execute Cells:**
   - Run the cells sequentially to extract text, generate embeddings, and build the vector index.
   - Use the `generate_answer()` function to query the document.

## 🧠 Memory Optimization
This project is optimized for systems with **8GB RAM** and no **GPU**. 
- It uses page-by-page text extraction to prevent RAM spikes.
- It utilizes a quantized 1B parameter model via Ollama for efficient local inference.