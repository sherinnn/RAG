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