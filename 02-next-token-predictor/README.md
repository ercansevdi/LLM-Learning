# 02 — Next Token Predictor

Understanding logits, softmax probabilities, and next-token prediction in a causal language model.

## Overview

This is the second project in my **LLM-Learning** series.

The goal is to understand one of the core mechanisms behind Large Language Models:

> Given the previous tokens, what is the probability distribution over the next possible token?

Instead of generating a full paragraph, this project directly inspects the model output and shows the most likely next-token candidates.

## Objectives

- Load a causal language model with Hugging Face Transformers.
- Convert input text into token IDs.
- Run a forward pass through the model.
- Inspect the model's logits.
- Convert logits into probabilities using softmax.
- Retrieve the Top-K most probable next tokens.
- Understand how context changes the next-token distribution.

## Model

This project uses:

`Qwen/Qwen2.5-0.5B`

The base model is used instead of an instruction-tuned model so that the fundamental next-token prediction behavior can be observed directly.

## Development Environment

This project is designed to run in **Google Colab**.

Recommended runtime:

```text
Google Colab
Runtime type: GPU
GPU: T4 or equivalent
```

## Installation

In Google Colab:

```python
!pip uninstall -y torchvision -q
!pip install -q -U transformers accelerate
```

After installation, restart the Colab runtime if necessary.

## Core Pipeline

```text
Input Text
    ↓
Tokenizer
    ↓
Token IDs
    ↓
Causal Language Model
    ↓
Logits
    ↓
Softmax
    ↓
Probability Distribution
    ↓
Top-K Next Tokens
```

## Key Concept: Causal Language Modeling

A causal language model estimates:

```text
P(x_t | x_1, x_2, ..., x_(t-1))
```

In other words:

> What is the probability of the next token given all previous tokens?

This is the basic mechanism behind autoregressive text generation.

## Logits

The model does not directly output probabilities.

It first produces raw numerical scores called **logits**.

Example:

```text
Token A → 8.42
Token B → 6.31
Token C → 3.11
```

These scores are not probabilities yet.

## Softmax

Softmax converts logits into a probability distribution:

```text
Logits
   ↓
Softmax
   ↓
Probabilities
```

Mathematically:

```text
P_i = exp(z_i) / Σ exp(z_j)
```

where:

- `z_i` is the logit of token `i`
- `P_i` is its probability

## Important Tensor Selection

The following line is central to this project:

```python
next_token_logits = outputs.logits[0, -1, :]
```

Meaning:

```text
0   → first item in the batch
-1  → final token position
:   → all vocabulary entries
```

So this extracts:

> The model scores for every possible token that could come next.

## Example Code

```python
import torch
from transformers import AutoTokenizer, AutoModelForCausalLM

MODEL_NAME = "Qwen/Qwen2.5-0.5B"

device = "cuda" if torch.cuda.is_available() else "cpu"

tokenizer = AutoTokenizer.from_pretrained(MODEL_NAME)

model = AutoModelForCausalLM.from_pretrained(
    MODEL_NAME,
    torch_dtype=torch.float16 if device == "cuda" else torch.float32
)

model = model.to(device)
model.eval()
```

## Next-Token Prediction Function

```python
def predict_next_tokens(text, top_k=10):
    inputs = tokenizer(text, return_tensors="pt")
    inputs = {
        key: value.to(device)
        for key, value in inputs.items()
    }

    with torch.no_grad():
        outputs = model(**inputs)

    next_token_logits = outputs.logits[0, -1, :]
    probabilities = torch.softmax(next_token_logits, dim=-1)
    top_probs, top_ids = torch.topk(probabilities, k=top_k)

    print("=" * 70)
    print("INPUT:")
    print(text)
    print("\nNEXT TOKEN CANDIDATES")
    print("-" * 70)

    for rank, (token_id, probability) in enumerate(
        zip(top_ids, top_probs),
        start=1
    ):
        token = tokenizer.decode([token_id.item()])
        print(
            f"{rank:2}. "
            f"{repr(token):20} "
            f"{probability.item()*100:8.3f}%"
        )
```

## Example Experiments

```python
predict_next_tokens("Yapay zeka gelecekte")
```

```python
predict_next_tokens(
    "Elektrik motorunda aşırı sıcaklık tespit edildi ve"
)
```

```python
predict_next_tokens(
    "Bir rulman arızasının en yaygın nedeni"
)
```

## Context Experiment

The model can also be tested with increasingly specific context:

```text
Motor
```

```text
Elektrik motoru
```

```text
Elektrik motorunda arıza
```

```text
Elektrik motorunda aşırı akım arızası meydana
```

As context becomes more specific, the probability distribution over the next token changes.

This demonstrates an important property of LLMs:

> Next-token prediction is conditional on the entire preceding context.

## Project Structure

```text
02-next-token-predictor/
│
├── README.md
├── next_token_predictor.ipynb
├── next_token_predictor.py
└── requirements.txt
```

## What I Learned

After completing this project, I can explain:

- What a causal language model is.
- What logits are.
- Why logits are not probabilities.
- How softmax converts logits into probabilities.
- How Top-K selection works.
- How to inspect the final-token logits.
- How context changes next-token probabilities.
- Why autoregressive text generation can be understood as repeated next-token prediction.

## Relationship to Text Generation

A simplified view of text generation is:

```text
Next-Token Predictor
        +
Repeated Prediction Loop
        =
Text Generation
```

The next project will extend this idea by repeatedly selecting and appending tokens.

## LLM-Learning Progress

**Project 02 / 30**

Previous project:

- 01 — Tokenizer Explorer

Next project:

- 03 — Hugging Face Text Generator
