# 05 — Text Summarization

Building an abstractive text summarization application with an instruction-tuned Large Language Model.

## Overview

This is the fifth project in my **LLM-Learning** series.

The first four projects focused on how LLM inference works:

- tokenization
- next-token prediction
- text generation
- generation control

This project moves into a real NLP task:

> Summarizing a longer source text into a shorter representation while preserving the main information.

## Objectives

- Build a reusable text summarization function.
- Understand extractive vs. abstractive summarization.
- Create short, technical, bullet-point, and simple-language summaries.
- Measure token-based compression ratio.
- Observe how prompts change summary style.
- Understand hallucination and factual consistency risks.
- Reuse controlled generation concepts from previous projects.

## Model

`Qwen/Qwen2.5-0.5B-Instruct`

## Development Environment

Designed for **Google Colab** with a GPU runtime.

## Installation

```python
!pip uninstall -y torchvision -q
!pip install -q -U transformers accelerate
```

## Extractive vs. Abstractive Summarization

**Extractive summarization** selects important parts directly from the source.

**Abstractive summarization** generates a new, shorter representation of the source information.

This project focuses on **abstractive summarization**.

## Core Pipeline

```text
Source Text
    ↓
Prompt / Instruction
    ↓
Chat Template
    ↓
Tokenizer
    ↓
Qwen Instruct Model
    ↓
Controlled Generation
    ↓
Generated Token IDs
    ↓
Decode
    ↓
Summary
```

## Why `do_sample=False`?

Summarization usually benefits from consistency and factual stability more than creativity.

```python
do_sample=False
```

This connects directly to **Project 04 — Generation Playground**.

## Example Experiments

### Standard Summary

```python
summarize_text(text)
```

### One-Sentence Summary

```python
summarize_text(
    text,
    instruction="Bu metni yalnızca tek cümleyle özetle."
)
```

### Three Bullet Points

```python
summarize_text(
    text,
    instruction="Metindeki en önemli bilgileri 3 maddelik bir liste halinde özetle."
)
```

### Technical Summary

```python
summarize_text(
    text,
    instruction="Bir elektrik-elektronik mühendisi için kısa teknik özet hazırla."
)
```

## Compression Ratio

```python
compression_ratio = len(summary_tokens) / len(input_tokens)
```

This gives the summary length relative to the source in token terms.

## Hallucination Risk

A generated summary may sound correct while introducing information that does not exist in the source.

A good summary should therefore be evaluated for both:

```text
Compression
+
Faithfulness
```

## Project Structure

```text
05-text-summarization/
├── README.md
├── text_summarization.py
├── text_summarization.ipynb
├── requirements.txt
└── .gitignore
```

## What I Learned

- Extractive vs. abstractive summarization
- Prompt-controlled summary styles
- Controlled decoding for technical summarization
- Token-based compression ratio
- Hallucination risk
- Factual consistency and faithfulness

## LLM-Learning Progress

**Project 05 / 30**

Next project:

- 06 — Question Answering Bot
