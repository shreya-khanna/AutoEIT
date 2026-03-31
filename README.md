# AutoEIT Test II – Automated Scoring of Elicited Imitation Task
Shreya Khanna
Submission for HumanAI's AutoEIT project for Google Summer of Code 26 

## Overview

This project implements a reproducible automated scoring pipeline (RAG-style)for the Spanish Elicited Imitation Task (EIT). The system compares learner transcriptions to target stimulus sentences and applies the Ortega (2000) meaning-based scoring rubric to assign sentence-level scores (0–4). The script processes participant data from Excel files and outputs scored results in a new Excel file while preserving the original dataset structure.


## Approach

The scoring system uses a hybrid approach combining rule-based processing and large language model (LLM)-based rubric scoring.

### Pipeline

1. **Input**: Excel file containing sentence number, target stimulus, and learner transcription
2. **Preprocessing**: Remove word-count hints and clean text for scoring
3. **Scoring**: Each pair is evaluated using the Ortega (2000) meaning-based rubric with deterministic LLM evaluation
4. **Output**: Scores written to Excel with summary statistics

## Reproducibility Measures

- Temperature = 0 for deterministic output
- Scoring rubric included directly in prompts
- Retry logic for API failures
- Rate limiting for stable API behavior
- Structured Excel output and error logging

## Scoring Rubric (Ortega, 2000)

| Score | Description |
|-------|-------------|
| 0 | No meaningful reproduction |
| 1 | About half of meaning preserved |
| 2 | More than half of meaning preserved but incomplete |
| 3 | Meaning preserved with grammatical differences |
| 4 | Exact repetition |

## Evaluation Methods

- **Human–AI Agreement**: Cohen's kappa, Pearson correlation, score distribution comparison
- **Manual Verification**: Review borderline cases (e.g., scores 2 vs. 3)
- **Consistency Testing**: Verify deterministic output reproducibility

## How to Run

```bash
pip install openpyxl google-generativeai
export GEMINI_API_KEY="your_api_key_here"
python autoeit_scoring.py
```

Output: `AutoEIT_Scored_Output.xlsx`

### Output Format

| Column | Content |
|--------|---------|
| A | Sentence number |
| B | Stimulus sentence |
| C | Learner transcription |
| D | Automated score (0–4) |

## Technologies

- Python
- OpenPyXL
- Google Generative AI API
- JSON

## Future Improvements

- Fully rule-based scoring engine for transparency
- Machine learning model trained on human-scored EIT data
- Confidence scores for automated scoring
- Web interface for researchers
- Human-in-the-loop review for uncertain cases