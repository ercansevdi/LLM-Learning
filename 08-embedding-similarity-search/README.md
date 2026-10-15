# 08 — Embedding Similarity Search

This project introduces **text embeddings**, **cosine similarity**, and the foundations of **semantic retrieval**.

It is Project **08/30** in the `LLM-Learning` series.

## Goal

Convert text into numerical vectors and compare those vectors to find semantically similar sentences and documents.

```text
Text
  ↓
Embedding Model
  ↓
Vector
  ↓
Cosine Similarity
  ↓
Semantic Similarity Score
```

## Model

`sentence-transformers/paraphrase-multilingual-MiniLM-L12-v2`

This multilingual Sentence Transformer supports Turkish and produces a **384-dimensional embedding vector** for each sentence.

## Installation

```bash
pip install -U sentence-transformers
```

## Basic Example

```python
from sentence_transformers import SentenceTransformer
from sentence_transformers.util import cos_sim

MODEL_NAME = "sentence-transformers/paraphrase-multilingual-MiniLM-L12-v2"
model = SentenceTransformer(MODEL_NAME)

sentence1 = "Elektrik motorunda yüksek titreşim var."
sentence2 = "Motor normalden fazla vibrasyon yapıyor."

embedding1 = model.encode(sentence1)
embedding2 = model.encode(sentence2)

score = cos_sim(embedding1, embedding2).item()

print("Similarity:", round(score, 4))
```

## What is an Embedding?

An embedding is a numerical representation of text.

```text
"Elektrik motorunda yüksek titreşim var."
                    ↓
             Embedding Model
                    ↓
[0.12, -0.45, 0.88, ...]
```

Texts with similar meanings tend to have vectors that are closer in embedding space.

## Cosine Similarity

Cosine similarity compares the direction of two vectors.

```text
Similar meaning
→ similar vector direction
→ higher cosine similarity
```

## Semantic Search Example

```python
query = "Motorda titreşim problemi var."

documents = [
    "Rulman arızası motor titreşiminde artışa neden olabilir.",
    "Motor sıcaklığının yükselmesi aşırı yükten kaynaklanabilir.",
    "PLC giriş modülleri dijital sensörlerden sinyal alır.",
    "Yağlama eksikliği rulman ömrünü azaltabilir.",
    "Bugün fabrikada bakım toplantısı yapılacaktır."
]

query_embedding = model.encode(query)
document_embeddings = model.encode(documents)

scores = cos_sim(
    query_embedding,
    document_embeddings
)[0]

for document, score in zip(documents, scores):
    print(round(score.item(), 4), "→", document)
```

## Reusable Semantic Search Function

```python
def semantic_search(query, documents, model):

    query_embedding = model.encode(query)
    document_embeddings = model.encode(documents)

    scores = cos_sim(
        query_embedding,
        document_embeddings
    )[0]

    results = []

    for index, score in enumerate(scores):
        results.append({
            "document": documents[index],
            "score": score.item()
        })

    return sorted(
        results,
        key=lambda x: x["score"],
        reverse=True
    )
```

## Keyword Search vs Semantic Search

A keyword-based system may treat these as different expressions:

```text
vibrasyon
titreşim
```

A semantic embedding model can detect that they are related in meaning.

## Important Distinction

This project does **not** use a generative LLM to answer questions.

```text
Embedding Model
→ Finds relevant information

Generative LLM
→ Generates an answer
```

The two components will later be combined in a RAG pipeline.

## Connection to RAG

```text
08 — Embedding Similarity
        ↓
09 — Semantic Document Search
        ↓
10 — Retrieval + LLM Generation
        ↓
       RAG
```

## What I Learned

- What a text embedding is
- How text is represented as a vector
- What embedding dimensionality means
- How cosine similarity compares embeddings
- Semantic similarity vs exact word matching
- How to rank documents by relevance
- The meaning of retrieval
- Why embeddings are important for RAG

## Project Structure

```text
08-embedding-similarity-search/
├── README.md
├── embedding_similarity_search.py
├── embedding_similarity_search.ipynb
└── requirements.txt
```

## LLM-Learning Progress

**Project 08 / 30**

Previous:
- 07 — Structured JSON Generator

Next:
- 09 — Semantic Document Search
