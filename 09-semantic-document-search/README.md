# 09 — Semantic Document Search / Anlamsal Doküman Arama

## Türkçe

Bu proje, küçük bir **semantic document search / anlamsal doküman arama** sistemi kurar.

Uzun dokümanlar önce küçük **chunk** parçalarına ayrılır. Her chunk bir embedding modelinden geçirilerek sayısal bir vektöre dönüştürülür. Kullanıcının sorusu da aynı embedding uzayına çevrilir ve **cosine similarity** kullanılarak sorguya en yakın doküman parçaları bulunur.

### Akış

```text
Dokümanlar
↓
Chunking
↓
Chunk Embeddings
↓
Kullanıcı Sorgusu
↓
Query Embedding
↓
Cosine Similarity
↓
Top-K Relevant Chunks
```

### Kullanılan model

`sentence-transformers/paraphrase-multilingual-MiniLM-L12-v2`

Model çok dillidir ve Türkçe metinlerle kullanılabilir.

### Temel kavramlar

- **Chunking:** Büyük dokümanı küçük bilgi parçalarına ayırma
- **Embedding:** Metni anlamsal bir sayısal vektöre dönüştürme
- **Cosine Similarity:** İki embedding arasındaki anlamsal yakınlığı ölçme
- **Top-K Retrieval:** En alakalı K sonucu seçme
- **Metadata:** Chunk'ın geldiği kaynak gibi ek bilgiler
- **Retriever:** Sorguya uygun context'i bulan sistem

Bu proje henüz cevap üretmez. Yalnızca ilgili bilgiyi bulur. Bir sonraki aşamada retrieved chunk'lar bir LLM'e verilerek RAG kurulacaktır.

---

## English

This project builds a small **semantic document search** system.

Long documents are first split into smaller **chunks**. Each chunk is converted into a numerical vector using an embedding model. The user query is encoded into the same embedding space, and **cosine similarity** is used to retrieve the most relevant document chunks.

### Pipeline

```text
Documents
↓
Chunking
↓
Chunk Embeddings
↓
User Query
↓
Query Embedding
↓
Cosine Similarity
↓
Top-K Relevant Chunks
```

### Model

`sentence-transformers/paraphrase-multilingual-MiniLM-L12-v2`

The model is multilingual and can be used with Turkish text.

### Key concepts

- **Chunking:** Splitting large documents into smaller information units
- **Embedding:** Converting text into a semantic numerical vector
- **Cosine Similarity:** Measuring similarity between embeddings
- **Top-K Retrieval:** Selecting the K most relevant results
- **Metadata:** Additional information such as the source document
- **Retriever:** The component that finds relevant context for a query

This project does not generate answers yet. It only retrieves relevant information. In the next step, the retrieved chunks can be passed to an LLM to create a RAG pipeline.

## Project Structure

```text
09-semantic-document-search/
├── semantic_document_search.ipynb
├── README.md
└── requirements.txt
```

## LLM-Learning Progress

**Project 09 / 30**

Previous:
- 08 — Embedding Similarity Search

Next:
- 10 — First RAG
