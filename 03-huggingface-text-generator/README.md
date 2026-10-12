# 03 — Hugging Face Text Generator

Building a simple text generation application with an instruction-tuned Large Language Model.

## Overview

This is the third project in my **LLM-Learning** series.

In the previous projects:

- **Project 01** explored tokenization and token IDs.
- **Project 02** explored logits, softmax, and next-token prediction.
- **Project 03** combines these ideas to generate complete text responses using an instruction-tuned language model.

The core idea is simple:

```text
Prompt
  ↓
Tokenizer
  ↓
Token IDs
  ↓
Language Model
  ↓
Next Token
  ↓
Append Token
  ↓
Repeat
  ↓
Generated Text
```

## Objectives

- Load an instruction-tuned model with Hugging Face Transformers.
- Understand the difference between base and instruct models.
- Use a chat template correctly.
- Generate text with `model.generate()`.
- Understand `max_new_tokens`.
- Separate prompt tokens from generated tokens.
- Decode generated token IDs back into readable text.
- Observe the limitations of a small language model.

## Model

This project uses:

`Qwen/Qwen2.5-0.5B-Instruct`

The instruction-tuned version is used because the goal is to respond to user prompts rather than simply continue raw text.

## Base Model vs. Instruct Model

A **base model** primarily learns to continue text.

An **instruct model** is further trained to follow user instructions.

Example:

```text
Base model:
"Artificial intelligence will..."
→ continues the text

Instruct model:
"Explain artificial intelligence."
→ attempts to answer the request
```

## Development Environment

This project is designed for **Google Colab**.

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

Restart the runtime if necessary.

## Load the Model

```python
import torch
from transformers import AutoTokenizer, AutoModelForCausalLM

MODEL_NAME = "Qwen/Qwen2.5-0.5B-Instruct"

device = "cuda" if torch.cuda.is_available() else "cpu"

tokenizer = AutoTokenizer.from_pretrained(MODEL_NAME)

model = AutoModelForCausalLM.from_pretrained(
    MODEL_NAME,
    torch_dtype=torch.float16 if device == "cuda" else torch.float32
)

model = model.to(device)
model.eval()

print("Model loaded.")
print("Device:", device)
```

## Why Chat Templates Matter

Instruction-tuned models are usually trained with structured conversation roles such as:

```text
SYSTEM
USER
ASSISTANT
```

Instead of sending raw text directly to the tokenizer, this project uses:

```python
tokenizer.apply_chat_template(...)
```

This converts the conversation into the format expected by the model.

## Text Generation Function

```python
def generate_text(prompt, max_new_tokens=150):

    messages = [
        {
            "role": "system",
            "content": (
                "You are a helpful technical assistant. "
                "Answer clearly, accurately, and concisely."
            )
        },
        {
            "role": "user",
            "content": prompt
        }
    ]

    inputs = tokenizer.apply_chat_template(
        messages,
        add_generation_prompt=True,
        tokenize=True,
        return_dict=True,
        return_tensors="pt"
    ).to(device)

    with torch.no_grad():

        outputs = model.generate(
            **inputs,
            max_new_tokens=max_new_tokens,
            do_sample=False
        )

    generated_tokens = outputs[0][inputs["input_ids"].shape[-1]:]

    answer = tokenizer.decode(
        generated_tokens,
        skip_special_tokens=True
    )

    return answer
```

## What `model.generate()` Does

A simplified view:

```text
Input Tokens
    ↓
Predict Next Token
    ↓
Append Token
    ↓
Predict Next Token
    ↓
Append Token
    ↓
Repeat
    ↓
Generated Sequence
```

So text generation can be understood as:

```text
Next-Token Prediction
        +
Repeated Generation Loop
        =
Text Generation
```

## `max_new_tokens`

Example:

```python
max_new_tokens=150
```

This means:

> Generate at most 150 new tokens after the input prompt.

It refers to tokens, not words.

## Removing the Prompt from the Output

`generate()` returns both the original input tokens and the newly generated tokens.

To keep only the generated answer:

```python
input_length = inputs["input_ids"].shape[-1]

generated_tokens = outputs[0][input_length:]
```

Then decode the generated part:

```python
answer = tokenizer.decode(
    generated_tokens,
    skip_special_tokens=True
)
```

## Example Experiments

```python
print(
    generate_text(
        "Elektrik motorlarında rulman arızasının üç yaygın nedenini açıkla."
    )
)
```

```python
print(
    generate_text(
        "TinyML nedir ve mikrodenetleyicilerde neden kullanılır?"
    )
)
```

```python
print(
    generate_text(
        "STM32 ile ESP32 arasındaki temel farkları açıkla."
    )
)
```

```python
print(
    generate_text(
        "Explain TinyML in simple English."
    )
)
```

## Small Model Observation

`Qwen2.5-0.5B-Instruct` is a relatively small language model.

Because of its limited parameter count, its answers may be:

- relevant but incomplete
- repetitive
- technically weak
- inconsistent
- occasionally incorrect

This is expected.

The purpose of this project is not to build a production-quality assistant. The main objective is to understand the inference and text-generation pipeline.

## Core Pipeline

```text
User Prompt
    ↓
Chat Template
    ↓
Tokenizer
    ↓
Token IDs
    ↓
Qwen2.5-0.5B-Instruct
    ↓
Autoregressive Generation
    ↓
Generated Token IDs
    ↓
Decode
    ↓
Readable Answer
```

## Project Structure

```text
03-huggingface-text-generator/
│
├── README.md
├── huggingface_text_generator.ipynb
├── huggingface_text_generator.py
└── requirements.txt
```

## What I Learned

After completing this project, I can explain:

- How text generation works in an autoregressive language model.
- The difference between a base model and an instruction-tuned model.
- Why chat templates are important.
- What `model.generate()` does.
- What `max_new_tokens` controls.
- How to separate prompt tokens from generated tokens.
- How token IDs are decoded back into text.
- Why small LLMs may generate relevant but low-quality answers.

## LLM-Learning Progress

**Project 03 / 30**

Previous projects:

- 01 — Tokenizer Explorer
- 02 — Next Token Predictor

Next project:

- 04 — Generation Playground
