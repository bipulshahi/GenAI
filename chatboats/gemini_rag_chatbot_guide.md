
# 💬 RAG-Based Chatbot with Gemini and Private PDF Data

This guide explains how to build a chatbot that answers questions from your **private PDF** using **Gemini 1.5 Flash**, **FAISS**, and **Sentence Embeddings**.

---

## 🧠 What You’ll Build

A **RAG (Retrieval-Augmented Generation)** system that:
1. Extracts text from a PDF.
2. Splits it into chunks.
3. Converts chunks into embeddings.
4. Stores them in FAISS.
5. Retrieves relevant chunks for a query.
6. Uses Gemini to generate answers.

---

## 📁 Step-by-Step Code with Explanation

### 1. **Specify PDF Path**

```python
pdf_path = "/content/DC_Training_Overview.pdf"  # Replace with your PDF path
```

### 2. **Extract Text from PDF**

```python
text = extract_text_from_pdf(pdf_path)
```

> **Example Output:**
> ```
> "DC Training helps employees understand the fundamentals of data center operations..."
> ```

---

### 3. **Chunk the Text**

```python
chunks = chunk_text(text)
```

> Splits long text into manageable 500-character chunks with overlaps.

---

### 4. **Generate Embeddings**

```python
embeddings = embed_chunks(chunks)
```

> Converts each chunk into a high-dimensional vector using a model like `sentence-transformers`.

---

### 5. **Build a FAISS Index**

```python
index = build_faiss_index(embeddings)
```

> Enables fast vector similarity search on your private data.

---

### 6. **User Query**

```python
query = "What is DC training?"
```

---

### 7. **Retrieve Relevant Chunks**

```python
context_chunks = get_top_k_chunks(query, index, chunks, model)
```

> Embeds the query, finds closest chunks using FAISS.

---

### 8. **Ask Gemini with Context**

```python
answer = ask_gemini(query, context_chunks)
print(answer)
```

> Uses Gemini (`gemini-1.5-flash`) to generate a response based on the relevant document context.

---

## 📊 Pipeline Summary

| Step            | Purpose                            | Tool Used               |
|------------------|-------------------------------------|--------------------------|
| PDF Extraction   | Read text from your private files   | PyPDF2                   |
| Chunking         | Manage token size and relevance     | Langchain splitters      |
| Embedding        | Semantic search capability          | Sentence Transformers    |
| Indexing         | Fast retrieval                      | FAISS                    |
| Retrieval        | Get context for a query             | FAISS + Embedding search |
| Generation       | Create final answer                 | Gemini API               |

---

## ✅ Example Output

**Query:** `What is DC training?`  
**Gemini Response:**  
> DC Training is a program designed to educate employees about data center fundamentals, including power systems, cooling infrastructure, security protocols, and maintenance best practices.

---

## 🚀 Next Steps

- Add a UI with Streamlit or Gradio
- Scale with multiple documents
- Deploy on the web (using FastAPI or Flask backend)
