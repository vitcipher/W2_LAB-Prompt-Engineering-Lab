# W2 LAB — Prompt Engineering Lab

Diagnosing and fixing an unreliable customer-service chatbot for "TechFlow Solutions" by systematically testing and improving prompts for three tasks — sentiment analysis, product description generation, and data extraction.

## Repository map

| File | Purpose |
|---|---|
| `prompt_engineering_lab.ipynb` | The full lab: helper functions, prompt versions v1/v2/v3 for each task, 5/10/15-run tests, failure analysis with consistency metrics, task variations (Part 5), and the final comparison report. |
| `lab_summary.md` | One-paragraph narrative summary of what was tried, what improved, and lessons learned. |
| `README.md` | This file. |

## How to run

1. Requirements: Python 3.10+, `openai`, `python-dotenv`, Jupyter.
   ```bash
   pip install openai python-dotenv jupyter
   ```
2. Create a `.env` file in the repository root (it is git-ignored) containing:
   ```
   OPENAI_API_KEY=your-key-here
   ```
3. Open `prompt_engineering_lab.ipynb` and run all cells top to bottom.

Notes:

- The notebook makes several hundred API calls to `gpt-4o-mini` (each multi-run test calls the API 5–15 times with a 1-second delay), so a full run takes ~15–25 minutes and a few cents of API credit.
- Outputs are non-deterministic: consistency percentages will vary slightly between full runs — that variability is exactly what the lab measures.

## Structure of the notebook

- **Part 1** — Environment setup, helper functions (`run_openai_request`, `run_multiple_requests`), naive zero-shot v1 prompts.
- **Part 2** — 5/10/15-run tests of the v1 prompts to expose failure patterns.
- **Part 3** — v2 prompts: explicit instructions, output formats, and constraints.
- **Part 4** — v3 prompts: few-shot examples (sentiment, product) and Chain-of-Thought (extraction).
- **Failure Analysis & Consistency Report** — 15-run scoring of all nine prompts on exact-match consistency and format adherence, with documented failure patterns and the v1 vs v3 comparison.
- **Part 5** — Reusable prompt templates tested on task variations (negative/neutral/mixed messages, different products, feedback with missing fields), plus the final evaluation report.
