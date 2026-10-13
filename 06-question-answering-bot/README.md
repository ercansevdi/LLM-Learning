# 06 — Question Answering Bot

A context-grounded question answering application built with an instruction-tuned Large Language Model.

## Overview

This is Project **06/30** in my **LLM-Learning** series. The goal is to answer questions using only a supplied source text and to avoid inventing information that is not supported by that source.

This project introduces the foundations of **grounded question answering**, which later leads directly to **Retrieval-Augmented Generation (RAG)**.

## Objectives

- Build a reusable context-based QA function.
- Understand closed-book vs. context-grounded question answering.
- Learn grounding and answerability.
- Observe hallucination and over-refusal behavior.
- See how model capacity affects instruction following.
- Connect prompt design to factual QA behavior.

## Model

`Qwen/Qwen2.5-1.5B-Instruct`

The project originally started with `Qwen/Qwen2.5-0.5B-Instruct`, but the smaller model showed weaker instruction-following behavior in the grounding tests.

## Environment

Designed for **Google Colab** with a GPU runtime.

```python
!pip uninstall -y torchvision -q
!pip install -q -U transformers accelerate
```

## Core Pipeline

```text
Context + Question
        ↓
   Chat Template
        ↓
     Tokenizer
        ↓
       LLM
        ↓
Grounded Answer
```

## Grounded QA

The model receives both a context and a question. It is instructed to use only information from that context.

If the answer cannot be found, the expected response is:

```text
Bu bilgi verilen kaynakta bulunmuyor.
```

## Core Function

```python
def ask_question(context, question, max_new_tokens=100):
    messages = [
        {
            "role": "system",
            "content": (
                "Answer the question using only the provided context. "
                "Do not use outside knowledge. "
                "If the answer cannot be found in the context, reply exactly: "
                "'Bu bilgi verilen kaynakta bulunmuyor.' "
                "If the answer exists in the context, answer briefly in Turkish."
            )
        },
        {
            "role": "user",
            "content": f"KAYNAK:\n{context}\n\nSORU:\n{question}"
        }
    ]
```

Generation uses:

```python
do_sample=False
```

because factual QA benefits from consistent decoding rather than creative sampling.

## Key Experiment

This project produced a useful sequence of failure cases.

### 1. Small model + loose prompt

`Qwen2.5-0.5B-Instruct` was asked:

```text
Motor kaç amper çeker?
```

The source contained no current information, but the model answered approximately:

```text
1000 A
```

This is a clear **hallucination**.

### 2. Small model + overly strict prompt

The prompt was made much stricter. The model then began returning:

```text
Bu bilgi verilen kaynakta bulunmuyor.
```

even when the answer actually existed in the source.

This demonstrates **over-refusal**.

### 3. Small model + few-shot prompting

Examples were added to the prompt, but the 0.5B model sometimes confused the examples with the real source context.

### 4. Larger model + simpler prompt

The model was changed to:

```text
Qwen2.5-1.5B-Instruct
```

and the prompt was simplified.

The behavior became much more reliable:

```text
Answer exists in context
→ answer it

Answer is absent
→ say that it is not in the source
```

## Main Lesson

Prompt engineering alone cannot fully compensate for limited model capability.

```text
More capable model
+
Clearer prompt
+
Controlled decoding
=
Better grounded QA behavior
```

## Key Concepts

### Grounding

Constraining an LLM response to a specific information source.

### Answerability

Determining whether a question can actually be answered from the supplied context.

### Hallucination

Generating information that is unsupported by the source.

### Over-Refusal

Refusing to answer even when the necessary information is available in the context.

## Connection to RAG

In this project, the context is selected manually:

```text
Human selects context
        ↓
Context + Question
        ↓
       LLM
```

A RAG system adds automatic retrieval:

```text
Large document collection
        ↓
     Retriever
        ↓
Relevant context
        ↓
Context + Question
        ↓
       LLM
```

This project is therefore a simplified RAG pipeline **without the retrieval stage**.

## Project Structure

```text
06-question-answering-bot/
├── README.md
├── question_answering_bot.py
├── question_answering_bot.ipynb
├── requirements.txt
└── .gitignore
```

## What I Learned

- Closed-book vs. context-grounded QA
- Grounding
- Answerability
- Hallucination
- Over-refusal
- Instruction following
- Model capacity matters
- Simpler prompts can outperform overly complicated prompts
- Deterministic decoding is useful for factual QA
- How grounded QA leads toward RAG

## LLM-Learning Progress

**Project 06 / 30**

Next project: **07 — Structured JSON Generator**
