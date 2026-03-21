# 📚 The RAG Librarian

A high-resolution Retrieval-Augmented Generation (RAG) system designed to navigate complex literary works. This project evolved from a local CPU script into a **High-Performance Cloud Orchestrator** capable of running 7B-parameter models on constrained hardware (NVIDIA T4 15GB).

## 🚀 The "Surgical Search" Evolution
Unlike standard RAG pipelines that lose context in dense narratives, this Librarian uses a three-tier optimization strategy:

1. **Keyword Gating**: Uses LLM-generated "Surgical Anchors" to filter vector results, eliminating semantic drift.
2. **O(1) Neighbor Retrieval**: Replaces slow linear list-scanning with a **Dictionary Lookup Map**, turning a 90-second context-stitching bottleneck into a near-instant operation.
3. **Dynamic VRAM Handshake**: Manages GPU memory by swapping the Reranker and the LLM via `torch.cuda.empty_cache()`, allowing 7B models to fit on 15GB VRAM.

## 🧪 Model Performance Benchmarks
Tested on **Les Misérables** (approx. 4,700 chunks) using an NVIDIA T4 GPU:

| Notebook | Model | Latency | Reasoning Quality |
| :--- | :--- | :--- | :--- |
| `..._GPU_Phi35.ipynb` | **Phi-3.5 Mini (3.8B)** | **~75s** | **Elite**: Poetic, symbolic, and descriptive. |
| `..._GPU_Mistral7B.ipynb` | **Mistral 7B v0.3** | **~86s** | **High**: Analytical and deeply grounded. |
| `..._GPU.ipynb` | **Llama 3.2 (3B)** | **~81s** | **Good**: Fast and factually reliable. |

---

## 📁 Project Structure
```text
02_RAG_Librarian_Demo/
├── Library/                          # Source EPUBs/Text organized by Author
├── faiss_librarian_index/            # Persistent FAISS vector database
├── RAG_Librarian_Demo_Notebook_GPU_Phi35.ipynb    # Latest: Long-Context optimized
├── RAG_Librarian_Demo_Notebook_GPU_Mistral7B.ipynb # High-Reasoning 7B variant
├── RAG_Librarian_Demo_Notebook_GPU.ipynb           # Standard 3B Cloud variant
└── requirements.txt                  # Updated for BitsAndBytes & Transformers 2026
```
---

## 🛠️ Technical Stack

- **LLM Engines**: Mistral 7B v0.3, Phi-3.5 Mini (3.8B), Llama 3.2  
- **Vector Store**: FAISS (FlatL2)  
- **Embeddings**: BAAI/bge-small-en-v1.5  
- **Reranker**: BAAI/bge-reranker-base (GPU-Accelerated)  
- **Optimization**: 4-bit NF4 Quantization + Gradient Checkpointing  

---

## ⚙️ The Pipeline Logic

- **Ingestion**: 1200-char chunks with 300-char "Semantic Bridges" (overlap)  
- **Analyst Phase**: LLM extracts 5 verbatim anchors from the query using a strict chat template  
- **Surgical Search**: FAISS retrieves top 100; only those containing keywords survive  
- **Context Stitching**: O(1) lookup retrieves neighbors (radius 1–2) to reconstruct the scene  
- **GPU Handshake**: Reranker scores context, then clears VRAM for the LLM  
- **Synthesis**: The "Librarian" provides a grounded, literary answer with source metadata citations  

---

## 🔧 Setup

- **Hardware**: Recommended NVIDIA T4 (Google Colab / Kaggle)  
- **Install Pandoc**: Required for EPUB processing  

- **Dependencies**:
```bash
pip install -r requirements.txt
```
- **Model Note**:  
  Phi-3.5 requires `trust_remote_code=False` to maintain compatibility with modern DynamicCache implementations.

---

## 📚 Literary Benchmarking: The "Gavroche" Test

To demonstrate the "Semantic Leap" between models, we asked:

> *"Describe the moment Gavroche was singing at the barricade while collecting cartridges. What was the 'will-o'-the-wisp' comparison?"*

| Model | Response Style | Depth of Analysis |
|-------|----------------|------------------|
| **Llama 3.2 (1B/3B)** | Functional | Identifies the scene and action, focuses on the "what" but misses deeper metaphor |
| **Mistral 7B v0.3** | Analytical | Explains the metaphor as elusiveness and battlefield frustration |
| **Phi-3.5 Mini** | Poetic / Symbolic | **Librarian’s Choice**: Connects to folklore and portrays a "trickster archetype" |

These results highlight the importance of model selection in Retrieval-Augmented Generation systems. While smaller models like Llama 3.2 provide fast and reliable factual grounding, larger or more specialized models such as Mistral 7B and Phi-3.5 Mini demonstrate a clear advantage in interpretive depth and contextual reasoning. In literary applications, where nuance, symbolism, and narrative understanding are critical, this difference becomes especially pronounced, positioning Phi-3.5 Mini as the preferred choice for high-quality, human-like synthesis despite similar latency constraints.