# LLM-Learning

A structured, hands-on learning repository focused on **Large Language Models, NLP, RAG, fine-tuning, evaluation, agents, and production LLM systems**.

This repository documents my progression from fundamental LLM concepts to advanced LLM engineering through **30 practical projects**.

## Objective

The goal of this repository is not only to learn how to use LLMs, but to understand how modern LLM systems work end-to-end:

```text
Text
  ↓
Tokenization
  ↓
Embeddings
  ↓
Transformer
  ↓
Inference
  ↓
RAG
  ↓
Fine-Tuning
  ↓
Evaluation
  ↓
Agents
  ↓
Deployment
```

The first milestone is to complete all **30 projects** in this repository.

After this learning series, larger production-grade and job-oriented projects will be developed as separate repositories.

---

## Progress

**Completed: 1 / 30**

```text
[█                             ] 3%
```

---

## 30-Project Roadmap

| # | Project | Main Focus | Status |
|---|---|---|---|
| 01 | [Tokenizer Explorer](./01-tokenizer-explorer/) | Tokenization, token IDs, encoding/decoding | ✅ Completed |
| 02 | Next Token Predictor | Autoregressive language modeling basics | ⬜ Planned |
| 03 | Hugging Face Text Generator | Transformers inference and text generation | ⬜ Planned |
| 04 | Generation Playground | Temperature, top-k, top-p, max tokens | ⬜ Planned |
| 05 | Text Summarization | Prompting and summarization inference | ⬜ Planned |
| 06 | Question Answering Bot | Instruction-following and QA | ⬜ Planned |
| 07 | Structured Output Generator | JSON and structured LLM outputs | ⬜ Planned |
| 08 | Embedding Similarity Search | Embeddings and cosine similarity | ⬜ Planned |
| 09 | Semantic Document Search | Vector search and retrieval | ⬜ Planned |
| 10 | Chat with PDF | Basic RAG pipeline | ⬜ Planned |
| 11 | Multi-PDF RAG | Chunking, metadata and retrieval | ⬜ Planned |
| 12 | RAG with Citations | Grounded answers and source attribution | ⬜ Planned |
| 13 | Turkish Academic RAG | Turkish embeddings and reranking | ⬜ Planned |
| 14 | Industrial Manual Assistant | Industrial RAG application | ⬜ Planned |
| 15 | Local LLM Chat | GGUF and llama.cpp inference | ⬜ Planned |
| 16 | Quantization Comparison | FP16, INT8 and INT4 comparison | ⬜ Planned |
| 17 | Transformer from Scratch | Attention, FFN, residuals and normalization | ⬜ Planned |
| 18 | Mini GPT from Scratch | Training a small causal language model | ⬜ Planned |
| 19 | LoRA Fine-Tuning | Parameter-efficient fine-tuning | ⬜ Planned |
| 20 | QLoRA Fine-Tuning | 4-bit training with LoRA | ⬜ Planned |
| 21 | Turkish Instruction Fine-Tuning | Instruction dataset preparation and tuning | ⬜ Planned |
| 22 | RAG vs Fine-Tuning | Comparative LLM experimentation | ⬜ Planned |
| 23 | LLM Evaluation Framework | Benchmarking and evaluation metrics | ⬜ Planned |
| 24 | Hallucination Detector | Grounding and faithfulness evaluation | ⬜ Planned |
| 25 | Tool-Calling Agent | Function calling and tool use | ⬜ Planned |
| 26 | Multi-Agent System | Agent coordination and orchestration | ⬜ Planned |
| 27 | LLM API Server | FastAPI and model serving | ⬜ Planned |
| 28 | Production RAG System | Hybrid search, reranking and caching | ⬜ Planned |
| 29 | Multimodal RAG | Text, image and table retrieval | ⬜ Planned |
| 30 | End-to-End LLM Platform | RAG, fine-tuning, evaluation, API and UI | ⬜ Planned |

---

## Repository Structure

```text
LLM-Learning/
│
├── README.md
├── LICENSE
├── .gitignore
│
├── 01-tokenizer-explorer/
│   ├── README.md
│   ├── tokenizer_explorer.py
│   ├── tokenizer_explorer.ipynb
│   └── requirements.txt
│
├── 02-next-token-predictor/
├── 03-huggingface-text-generator/
├── 04-generation-playground/
├── ...
└── 30-end-to-end-llm-platform/
```

Each project will contain its own documentation, source code, dependencies, experiments, and results when applicable.

---

## Standard Project Format

Each project should follow a consistent structure:

```text
project-name/
│
├── README.md
├── src/ or main.py
├── notebook.ipynb
├── requirements.txt
├── results/
└── screenshots/
```

Not every project requires every folder. The structure will be adapted according to the project.

---

## Learning Areas

This repository covers:

- Tokenization
- Hugging Face Transformers
- Prompting
- Text generation
- Embeddings
- Semantic search
- Vector databases
- Retrieval-Augmented Generation (RAG)
- Local LLM inference
- Quantization
- Transformer architecture
- Causal language modeling
- LoRA
- QLoRA
- Instruction fine-tuning
- LLM evaluation
- Hallucination detection
- Tool calling
- Agentic AI
- Multi-agent systems
- FastAPI
- Model serving
- Production RAG
- Multimodal LLM systems

---

## Technology Stack

The stack will evolve throughout the 30 projects.

Core technologies include:

```text
Python
Jupyter Notebook
PyTorch
Hugging Face Transformers
Hugging Face PEFT
Sentence Transformers
FAISS / Qdrant
FastAPI
llama.cpp
vLLM
Docker
Git / GitHub
```

Additional tools will be introduced when required by individual projects.

---

## Portfolio Strategy

This repository represents the **learning and experimentation layer** of my LLM portfolio.

Small and medium-scale exercises remain inside `LLM-Learning`.

Larger production-grade projects will be developed as independent repositories, including areas such as:

- Industrial RAG
- Industrial AI assistants
- Turkish LLM fine-tuning
- LLM evaluation platforms
- Agentic AI systems
- Local LLM serving
- Multimodal industrial assistants
- Production LLM infrastructure

---

## Engineering Focus

My long-term direction combines:

```text
Electrical / Electronics Engineering
                +
Industrial Automation
                +
Artificial Intelligence
                +
Large Language Models
```

The objective is to build LLM systems that solve real engineering and industrial problems rather than only generic chatbot applications.

---

## Current Project

### 01 — Tokenizer Explorer

Topics:

- Tokenizer
- Vocabulary
- Token IDs
- Encoding
- Decoding
- Subword tokenization
- Turkish morphology
- Turkish vs. English tokenization

Status: **Completed**

---

## Next Project

### 02 — Next Token Predictor

The next project will focus on the fundamental idea behind autoregressive language models:

```text
P(x_t | x_1, x_2, ..., x_(t-1))
```

The project will visualize the most probable next tokens for a given input sequence.

---

## Long-Term Goal

This repository is part of a broader two-year AI engineering portfolio.

The target is to build a large body of practical work while maintaining a smaller number of strong, production-grade flagship projects for CV and international job applications.

---

## Author

**Ercan Sevdi**

Electrical & Electronics Engineer  
Industrial Automation / Electronics Educator  
Artificial Intelligence M.Sc. Student

Focus areas:

- Large Language Models
- NLP
- TinyML
- Industrial AI
- Reinforcement Learning
- Robotics
- Data Science

---

## License

This repository is licensed under the MIT License.
