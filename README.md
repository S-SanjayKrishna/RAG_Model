# 📚 Gradio RAG Chatbot with Gemma + Qdrant + PyMuPDF

A lightweight Retrieval-Augmented Generation (RAG) chatbot using a local LLM (Gemma), vector storage via Qdrant, and a Gradio interface for interaction. Users can upload PDF documents, which are then chunked, embedded, stored, and used to answer queries contextually.

---

## 🚀 Features

- 🔍 Semantic search over PDF documents
- 🤖 Local LLM (Gemma) for response generation
- 📦 Vector storage using Qdrant (in-memory or remote)
- 🧠 Sentence Transformers for embeddings
- 📄 PDF parsing via PyMuPDF
- 🎛️ Gradio UI for document upload and chat

---



## 🏗️ Architecture

```
User ↔ Gradio UI
        ↓
    Upload PDF
        ↓
    Parse (PyMuPDF)
        ↓
  Chunking Strategy
        ↓
Embedding (SentenceTransformers)
        ↓
Store in Qdrant (local memory or persistent)
        ↓
User Query
        ↓
  Semantic Search via Qdrant
        ↓
 Retrieve Top Chunks
        ↓
Pass context + query to Gemma LLM
        ↓
Generate Answer
        ↓
  Show Response in Chat UI
```

---

## 🧩 Chunking Strategy

- PDF text is split into chunks of ~300-500 characters with 50-character overlap.
- This helps maintain context continuity across sections.
- Chunking is based on paragraph structure and token count.

---

## 🔍 Retrieval Approach

- Embeddings are generated via sentence-transformers (e.g., all-MiniLM or BGE variants).
- Top K similar vectors are retrieved from Qdrant using cosine similarity.
- Retrieved documents are concatenated into context for Gemma’s response generation.

---

## 💻 Hardware Requirements

Minimum:
- CPU with AVX support
- 8 GB RAM

Recommended:
- GPU with CUDA (for fast LLM inference)
- 16 GB+ RAM

---

## 📦 File Structure

```
├── app.py                # Main app
├── utils.py              # Helper functions (chunking, embedding)
├── requirements.txt      # Optional - dependency list
└── README.md             # This file
```

---

## ✅ Observations

- Using Qdrant enables fast retrieval even with large document sets.
- Chunk size significantly affects performance and relevance — too small loses context, too large overloads prompt.
- Gradio allows easy prototyping and deployment.

---


