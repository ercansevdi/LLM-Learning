# LLM-Learning

A hands-on learning portfolio by **Ercan Sevdi**, progressing from LLM fundamentals to practical LLM engineering through **30 projects**.

The series covers tokenization, text generation, embeddings, retrieval-augmented generation (RAG), local inference, Transformer internals, fine-tuning, evaluation, agents, and deployment. These are roadmap topics; the completed implementation currently covers Project 01.

**Progress: 1 / 30 completed**  
**Current:** [01 — Tokenizer Explorer](./01-tokenizer-explorer/README.md)  
**Next:** 02 — Next Token Predictor

## Completed Project

### [01 — Tokenizer Explorer](./01-tokenizer-explorer/README.md)

A Jupyter notebook using the `Qwen/Qwen2.5-0.5B-Instruct` tokenizer to explore:

- Subword tokens and token IDs.
- Encoding text and decoding it back.
- Turkish word forms and their token counts.
- A Turkish / English sentence comparison.
- Industrial examples involving motors, TinyML, and smart factories.

[Open the notebook](./01-tokenizer-explorer/tokenizer_explorer.ipynb) · [Read the project guide](./01-tokenizer-explorer/README.md)

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

## Files Currently in This Repository

```text
LLM-Learning/
├── README.md
├── .gitignore
└── 01-tokenizer-explorer/
    ├── README.md
    └── tokenizer_explorer.ipynb
```

Projects 02–30 are planned. Their folders will be added when implementation starts. Project 01 is currently notebook-based; a standalone Python script, `requirements.txt`, and a repository `LICENSE` file have not been added.

## Run Project 01

See the [Project 01 setup and usage guide](./01-tokenizer-explorer/README.md#run-the-notebook) for the complete instructions. Open its notebook in Jupyter or Google Colab and execute the cells in order.

The current project uses Python, Jupyter, and Hugging Face Transformers. Other technologies will be introduced as the roadmap advances.

## Portfolio Strategy

Small and medium learning projects stay in this repository. Larger independent portfolio applications will have their own repositories after this learning series.

My direction combines electrical and electronics engineering, industrial automation, and AI, with an emphasis on engineering and industrial use cases.

## Author

**Ercan Sevdi**  
Electrical & Electronics Engineer · Industrial Automation / Electronics Educator · Artificial Intelligence M.Sc. Student
