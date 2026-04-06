# 🧠 Embeddings, Retrieval, and RAG — Complete Guide

Understanding **embeddings**, **semantic search**, and the **RAG (Retrieval-Augmented Generation)** pipeline.

---

## 📌 Table of Contents

- [What are Embeddings?](#-1-what-are-embeddings)
- [Cosine Similarity](#-cosine-similarity)
- [Top-K Retrieval](#-top-k-retrieval)
- [RAG Pipeline](#-rag-pipeline)
- [Vector Databases](#-vector-databases)
---

## 🧠 1. What are embeddings?

Embeddings are **numerical vector representations of text** that capture semantic meaning.

👉 Example:
- "cat" → [0.21, -0.45, 0.88, ...]
- "dog" → [0.19, -0.40, 0.91, ...]

---


Similar meanings → similar vectors.

---

## 🔢 2. Why convert text into embeddings?

Computers process numbers, not words.

Embeddings allow:
- Semantic comparison
- Mathematical similarity
- Efficient search

---

## 📐 Cosine Similarity

Formula:

\[
\cos(\theta) = \frac{A \cdot B}{\|A\| \|B\|}
\]

### 📊 Interpretation

| Value | Meaning |
|------|--------|
| 1    | Very similar |
| 0    | Unrelated |
| -1   | Opposite |

---

## ✂️ Text Chunking

Splitting large text into smaller pieces.

### ⚖️ Tradeoffs

| Chunk Size | Problem |
|----------|--------|
| Too small | Not enough context |
| Too large | Mixed topics, poor precision |

### ✅ Ideal Size
**200–500 tokens**

---

## 🔍 Top-K Retrieval

Instead of 1 result, retrieve **k best matches**.

### Why it matters:
- Better coverage
- Reduces missed information
- Improves answer quality

---

## 🧱 RAG Pipeline

```mermaid
flowchart TD
    A[Documents] --> B[Chunking]
    B --> C[Embeddings]
    C --> D[Vector Database]

    E[User Query] --> F[Query Embedding]
    F --> G[Similarity Search]
    D --> G

    G --> H[Top-K Chunks]
    H --> I[LLM]
    I --> J[Final Answer]

```
#### Step-by-step:
1. Split documents into chunks
2. Convert chunks into embeddings
3. Store in vector database
4. Embed user query
5. Compute similarity
6. Retrieve top-k chunks
7. Generate answer with LLM

## 📦 Vector Databases

A vector database stores embeddings and enables fast similarity search.

Popular options:
- FAISS
- Pinecone
- Weaviate
- Chroma

```mermaid
flowchart LR
    Q[Query] --> QE[Embedding]
    QE --> S[Similarity Comparison]
    S --> R[Top-K Results]
```

#### Steps:

- Convert query → embedding
- Compare with stored vectors
- Rank by similarity
- Return best matches

## 🔗 Why Embeddings Matter
- Capture meaning (not just keywords)
- Enable semantic search
- Improve retrieval accuracy

## 🧠 Why RAG Reduces Hallucinations

RAG grounds responses in real retrieved data, instead of relying only on training knowledge.

| System | Behavior                       |
| ------ | ------------------------------ |
| LLM    | Uses training data only        |
| RAG    | Uses external + retrieved data |

```mermaid
sequenceDiagram
    User->>System: Ask question
    System->>Embedding Model: Convert to vector
    System->>Vector DB: Search similar vectors
    Vector DB-->>System: Return top-k chunks
    System->>LLM: Provide context
    LLM-->>User: Answer
```

## 🧠 Why Similarity Scores Matter

- They rank relevance
- Prioritize best context
- Improve final answers