## ✂️ Text Chunking

Splitting large text into smaller pieces.

## Why do chunking?

Embedding an entire document at once is a bad idea because:
   - Long docs exceed model input limits
   - one huge vector loses local detail
   - search results are better when each chunk is focused

Embedding APIs and models have input limits, so chunk size matters. OpenAI’s embeddings reference explicitly notes that input must stay within the model’s maximum token limits

### ⚖️ Tradeoffs

| Chunk Size | Problem |
|----------|--------|
| Too small | Not enough context |
| Too large | Mixed topics, poor precision |

### ✅ Ideal Size
**200–500 tokens**


## 🔑 Chunking Strategies

### 1. Fixed-size chunking
Split every **N tokens** (e.g., 300)

👉 Pros:
- Simple
- Fast

❌ Cons:
- Can break meaning mid-sentence

---

### 2. Sentence / Paragraph-based chunking

Split using natural boundaries.

👉 Pros:
- Better semantic meaning

❌ Cons:
- Uneven chunk sizes

---

### 3. Sliding Window (Overlapping chunks)

Example:
- Chunk 1: tokens 0–300
- Chunk 2: tokens 250–550


👉 Pros:
- Preserves context across chunks  
- Very common in production RAG  

---

## 🔥 Advanced Tip: Structure-Aware Chunking

👉 This is what **senior engineers actually do**

Instead of:
- Blind token splitting

Do:
- Split based on structure

### Example (FAQ)

Instead of breaking randomly:
```
Q: What is RAG?
A: Retrieval-Augmented Generation...
```

👉 Keep each **Q&A pair as one chunk**

✅ Benefits:
- Cleaner embeddings  
- Better retrieval accuracy  
- More meaningful context  

---

## 📏 Token Limits & Chunk Sizes

Why chunk size matters even more:

### 🔑 Constraints

1. **Embedding model limits**
   - Example: 8k tokens max input

2. **LLM context window**
   - Includes:
     - Query
     - Retrieved chunks
     - Prompt

---

### ⚖️ Tradeoffs

- Small chunks → lose context  
- Large chunks → lose precision  

👉 New constraint:
- Too many chunks → exceed context window  


---
