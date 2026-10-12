# 04 — Generation Playground

Exploring how generation parameters change the behavior of an instruction-tuned Large Language Model.

## Overview

This is the fourth project in my **LLM-Learning** series.

The goal is to understand how token selection can be controlled during text generation using:

- `temperature`
- `top_k`
- `top_p`
- `do_sample`
- `repetition_penalty`

The same prompt is generated multiple times with different parameter settings so that the effect of each decoding strategy can be observed directly.

## Model

This project uses:

`Qwen/Qwen2.5-0.5B-Instruct`

## Development Environment

Designed for **Google Colab**.

Recommended runtime:

```text
Google Colab
Runtime type: GPU
GPU: T4 or equivalent
```

## Installation

```python
!pip uninstall -y torchvision -q
!pip install -q -U transformers accelerate
```

Restart the runtime if necessary.

## Core Pipeline

```text
Prompt
  ↓
Chat Template
  ↓
Tokenizer
  ↓
LLM
  ↓
Logits
  ↓
Temperature
  ↓
Top-K / Top-P Filtering
  ↓
Sampling
  ↓
Selected Token
  ↓
Repeat
  ↓
Generated Answer
```

## Generation Function

```python
def generate_text(
    prompt,
    temperature=0.7,
    top_k=20,
    top_p=0.8,
    repetition_penalty=1.1,
    max_new_tokens=150
):
    ...
```

## Temperature

Temperature controls how sharp or flat the token probability distribution becomes.

Low temperature:

```text
More conservative
More deterministic
Higher-probability tokens dominate
```

High temperature:

```text
More diverse
More random
Higher risk of weak or incorrect output
```

Example experiment:

```python
generate_text(prompt, temperature=0.2)
generate_text(prompt, temperature=0.7)
generate_text(prompt, temperature=1.3)
```

## Top-K

`top_k` limits sampling to the K most probable tokens.

Example:

```text
top_k = 5
→ sample only from the 5 strongest token candidates
```

Experiment:

```python
generate_text(prompt, top_k=5, top_p=1.0)
generate_text(prompt, top_k=20, top_p=1.0)
generate_text(prompt, top_k=100, top_p=1.0)
```

## Top-P

`top_p` uses nucleus sampling.

Instead of selecting a fixed number of token candidates, it keeps enough high-probability tokens to reach a target cumulative probability.

Example:

```text
top_p = 0.8
→ keep the smallest candidate set covering about 80% probability mass
```

Experiment:

```python
generate_text(prompt, top_k=0, top_p=0.5)
generate_text(prompt, top_k=0, top_p=0.8)
generate_text(prompt, top_k=0, top_p=0.95)
```

## `do_sample`

When:

```python
do_sample=False
```

the model behaves greedily and tends to choose the most likely continuation.

When:

```python
do_sample=True
```

the next token is sampled from the probability distribution.

This makes outputs more variable.

## Repetition Penalty

`repetition_penalty` helps reduce repeated tokens or phrases.

Example:

```python
generate_text(prompt, repetition_penalty=1.0)
generate_text(prompt, repetition_penalty=1.2)
```

`1.0` means no repetition penalty.

## Three Generation Profiles

### Technical

```python
temperature=0.3
top_k=20
top_p=0.7
repetition_penalty=1.1
```

Goal: more controlled output.

### Balanced

```python
temperature=0.7
top_k=20
top_p=0.8
repetition_penalty=1.1
```

Goal: balanced generation.

### Creative

```python
temperature=1.2
top_k=50
top_p=0.95
repetition_penalty=1.05
```

Goal: higher diversity.

These are experimental profiles, not universal best settings.

## Example Prompt

```text
Elektrik motorlarında rulman arızasının
üç yaygın nedenini açıkla.
```

The same prompt can be tested with multiple decoding configurations and compared.

## Project Structure

```text
04-generation-playground/
│
├── README.md
├── generation_playground.py
├── generation_playground.ipynb
├── requirements.txt
└── .gitignore
```

## What I Learned

After completing this project, I can explain:

- What temperature changes during generation.
- The difference between Top-K and Top-P.
- How sampling differs from greedy decoding.
- What `do_sample` controls.
- Why repetition penalties can be useful.
- Why decoding settings affect output quality and diversity.
- Why there is no single best generation configuration for every task.

## Learning Progress

**Project 04 / 30**

Previous projects:

- 01 — Tokenizer Explorer
- 02 — Next Token Predictor
- 03 — Hugging Face Text Generator

Next project:

- 05 — Text Summarization
