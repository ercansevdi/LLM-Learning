# 01 — Tokenizer Explorer

[← Back to LLM-Learning](../README.md)

**Status:** Completed learning exercise  
**Implementation:** [tokenizer_explorer.ipynb](./tokenizer_explorer.ipynb)  
**Tokenizer:** `Qwen/Qwen2.5-0.5B-Instruct`

## Purpose

Explore how text becomes tokens and token IDs before it reaches a language model. This notebook inspects Turkish and English examples, reconstructs text through decoding, and compares several Turkish word forms.

Only the tokenizer is loaded. The notebook does not load language-model weights, train a model, or generate text.

## What the Notebook Does

1. Installs / updates Hugging Face Transformers.
2. Loads the tokenizer with `AutoTokenizer.from_pretrained()`.
3. Prints its vocabulary information.
4. Tokenizes a Turkish sentence about bearing failure in electric motors.
5. Displays token IDs and matches them with token pieces.
6. Decodes the IDs back into the original sentence.
7. Compares Turkish word forms, from `motor` to `motorlarımızdakilerden`.
8. Compares token counts for a Turkish sentence and an English counterpart.
9. Defines a reusable `analyze_text(text)` function and applies it to TinyML and smart-factory examples.

## Run the Notebook

### Google Colab

1. Open Google Colab and upload `tokenizer_explorer.ipynb`.
2. Use a standard CPU runtime; GPU computation is not required for this tokenizer exercise.
3. Execute the cells from top to bottom. The first cell installs / updates `transformers`.
4. Allow internet access for the initial tokenizer download from Hugging Face.

### Local Jupyter

From this project directory, install the notebook tools and dependency:

```bash
python -m pip install jupyter transformers
python -m notebook tokenizer_explorer.ipynb
```

Run the notebook cells in order. It also includes `!pip install -U transformers`; package versions can change when this installation cell is rerun. A pinned dependency file has not been provided yet.

## Example Results Saved in the Notebook

The following values are taken from the uploaded notebook outputs, rather than a new execution during README review.

| Example | Whitespace-separated words | Tokens |
| --- | ---: | ---: |
| Elektrik motorlarında rulman arızası oluştu. | 5 | 15 |
| A bearing failure occurred in the electric motors. | 8 | 9 |
| STM32 mikrodenetleyicilerinde TinyML modeli çalıştırıyorum. | 5 | 19 |
| Akıllı fabrikalarda otonom taşıma araçları kullanılmaktadır. | 6 | 21 |

The first Turkish sentence was decoded back to the original text successfully.

### Turkish Word Forms

| Word | Tokens |
| --- | ---: |
| motor | 1 |
| motorlar | 2 |
| motorlardan | 3 |
| motorlarımızdan | 3 |
| motorlarımızdakilerden | 6 |

These examples show that word count and token count differ. The split depends on the tokenizer's vocabulary; it does not always follow grammatical suffix boundaries. The one sentence pair is an illustration, not a benchmark establishing a general language-wide difference.

## Read the Output Correctly

- `len(text.split())` counts whitespace-separated pieces, not linguistic words.
- Encoding examples use `add_special_tokens=False`.
- Decoding uses `skip_special_tokens=True`.
- Token strings can include byte-level markers such as `Ġ` and encoded-looking character sequences. Read them as internal token representations; use `decode()` to reconstruct readable text.
- The saved outputs report `len(tokenizer) = 151665` and a base `vocab_size = 151643`. The total includes added tokens, so these two values need not match.

## Try Your Own Text

After running the setup and function-definition cells, call:

```python
analyze_text("Buraya incelemek istediğin metni yaz.")
```

The function prints the word count, token count, token / ID pairs, and decoded text. Change `test_words` to inspect other Turkish word forms.

## Files

| File | Purpose |
| --- | --- |
| `README.md` | Project-specific setup, experiments, results, and limitations. |
| `tokenizer_explorer.ipynb` | Code cells and saved experiment outputs. |

Possible future additions include a standalone `.py` script, pinned dependencies, and comparisons across several tokenizers. These are not part of the current implementation.

[Return to the 30-project roadmap](../README.md#30-project-roadmap)
