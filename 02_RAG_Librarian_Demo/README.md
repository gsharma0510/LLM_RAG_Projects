# The RAG Librarian
This project is a high-resolution Retrieval-Augmented Generation (RAG) system designed to navigate and query complex literary works. Unlike standard RAG pipelines that often lose context in dense narratives, this modular Librarian uses a "Surgical Search" approach combined with "Neighbor Retrieval" to ensure the LLM understands not just the words, but the narrative moment.

## 🚀 Key Features
***Surgical Filtering***: Uses LLM-generated keywords to filter vector search results, eliminating "Semantic Drift" where the AI gets distracted by similar descriptions in the wrong chapters.

***Neighbor Retrieval***: When a relevant "needle" is found, the system automatically pulls the preceding and following chunks to provide the LLM with full narrative context (Description + Action + Dialogue).

***Local-First Architecture***: Runs entirely on local hardware using FAISS, Hugging Face Transformers, and Ollama, ensuring privacy and no API costs.

***Hybrid Reranking***: Combines the speed of BGE-Small embeddings with the deep reasoning of a BGE-Base Cross-Encoder reranker.

## 📁 Project Structure

```
02_RAG_Librarian_Demo/
├── Library/                         # Source epubs/text organized by Author
├── faiss_librarian_index/           # Local vector database (Git ignored)
├── RAG_Librarian_Demo_Notebook.ipynb # Main pipeline logic
├── requirements.txt                 # Python dependencies
└── .gitignore                       # Project-specific exclusion rules
```

## 🛠️ Technical Stack

**Vector Store**: *FAISS (FlatL2/Inner Product)*

**Embeddings**: *BAAI/bge-small-en-v1.5*

**Reranker**: *BAAI/bge-reranker-base*

**LLM Engine**: *Ollama (Running llama3.2:1b)*

**Document Processing**: *UnstructuredEPubLoader & Pandoc*

## ⚙️ How It Works

**Ingestion**: Books are split into 1200-character chunks with a 300-character overlap.

**Keyword Assistance**: The user's query is processed by a local LLM to extract unique identifiers (e.g., "Digne", "Passport").

**Vector Search**: FAISS retrieves the top 100 candidate chunks.

**Surgical Filter**: Chunks are stripped away if they do not contain the assistant's keywords.

**Context Expansion**: The system identifies the original_index of surviving chunks and retrieves their neighbors to fill in descriptive gaps.

**Reranking & Synthesis**: The Cross-Encoder ranks the expanded contexts, and the final top results are sent to Llama 3.2 for a precise, literary answer.

## 🔧 Setup & Installation

* **Install Pandoc**: Required for epub processing.

* **Setup Environment**:
```
Bash
pip install -r requirements.txt
```
* **Run Ollama**: Ensure Ollama is running locally with the command ollama run llama3.2:1b.

* **Index Your Library**: Run the ingestion cells in the notebook to create your faiss_librarian_index.