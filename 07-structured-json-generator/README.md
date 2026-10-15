# 07 — Structured JSON Generator

A structured-output project that converts technical natural-language descriptions into machine-readable JSON using an instruction-tuned Large Language Model.

## Overview

This is Project **07/30** in the `LLM-Learning` series.

The goal is to move from free-form text generation to **structured output** that can be consumed by Python applications, APIs, databases, automation systems, and future tool-calling/agent workflows.

## Model

`Qwen/Qwen2.5-1.5B-Instruct`

## Development Environment

Designed for **Google Colab** with a GPU runtime.

## Main Pipeline

```text
Natural Language
      ↓
     LLM
      ↓
JSON-like Output
      ↓
Cleaning
      ↓
json.loads()
      ↓
Python Dictionary
      ↓
Validation
```

## Example Input

```text
Bir elektrik motorunda normalden yüksek titreşim ve
çalışma sıcaklığında artış gözlemlendi.
Bakım ekibi rulman bölgesinden anormal ses geldiğini de bildirdi.
```

## Target Output

```json
{
  "equipment": "electric_motor",
  "symptoms": [
    "high_vibration",
    "temperature_increase",
    "abnormal_noise"
  ],
  "possible_fault": "bearing_fault",
  "severity": "medium"
}
```

## Required Fields

- `equipment`
- `symptoms`
- `possible_fault`
- `severity`

The `symptoms` field must be a list.

Allowed `severity` values:

- `low`
- `medium`
- `high`

## Key Concepts

### Structured Output

Instead of unrestricted prose, the model is asked to return data in a predefined format.

### JSON Parsing

LLM output initially arrives as text.

```python
data = json.loads(result)
```

converts valid JSON text into a Python dictionary.

### Markdown Cleanup

Models may wrap JSON inside Markdown code fences such as ` ```json ... ``` `. These markers must be removed before parsing.

### Validation

A structured response should be checked at three levels:

```text
1. Syntax
   Is it valid JSON?

2. Structure
   Are all required fields present?

3. Semantics
   Are the values actually correct?
```

## Important Lesson

```text
Looks like JSON
≠
Valid JSON
≠
Valid structure
≠
Correct information
```

LLM output should always be validated before downstream software uses it.

## Why This Matters

Structured outputs are useful for:

- API integrations
- automation pipelines
- databases
- industrial monitoring
- maintenance alerts
- tool calling
- AI agents
- backend services

Example:

```text
Operator Message
      ↓
LLM
      ↓
Structured JSON
      ↓
Python Logic
      ↓
Maintenance Alert
```

## What I Learned

- Free-form text vs. structured generation
- JSON parsing with `json.loads()`
- Cleaning Markdown-wrapped JSON
- Basic schema-like validation
- Syntax vs. structure vs. semantic correctness
- Why machine-readable LLM output must be validated

## LLM-Learning Progress

**Project 07 / 30**

Previous:
- 06 — Question Answering Bot

Next:
- 08 — Embedding Similarity Search
