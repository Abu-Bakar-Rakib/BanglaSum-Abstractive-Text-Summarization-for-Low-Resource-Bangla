# BanglaSum: Abstractive Text Summarization for Low-Resource Bangla

Fine-tuning `mT5` on the Bengali subset of **XL-Sum** for abstractive news summarization, with full automatic evaluation (ROUGE-1/2/L, BERTScore), an extractive TextRank baseline for comparison, and comprehensive analysis.

## Overview

| | |
|---|---|
| **Task** | Abstractive text summarization (Bangla) |
| **Dataset** | [XL-Sum (Bengali)](https://huggingface.co/datasets/csebuetnlp/xlsum) — news articles |
| **Base model** | [`csebuetnlp/mT5_multilingual_XLSum`](https://huggingface.co/csebuetnlp/mT5_multilingual_XLSum) |
| **Metrics** | ROUGE-1/2/L, BERTScore (F1), with a TextRank extractive baseline for comparison |
| **Eval set** | 200 randomly sampled test articles |

## Results

| Metric | Score |
|---|---|
| ROUGE-1 | 0.2366 |
| ROUGE-2 | 0.0999 |
| ROUGE-L | 0.2097 |
| BERTScore F1 | 0.7586 |
| Avg. generated length | 14.78 words |
| Avg. reference length | 21.85 words |

The fine-tuned model is also benchmarked against a TextRank extractive baseline on a 50-sample subset (see `model_comparison.csv`).

## Pipeline

1. Load and explore the XL-Sum Bengali dataset (article/summary length distributions, compression ratio)
2. Tokenize with the mT5 tokenizer (max input 512 tokens, max target 128 tokens)
3. Fine-tune `mT5_multilingual_XLSum` with `Seq2SeqTrainer` (early stopping, beam search decoding)
4. Generate summaries on a held-out test sample
5. Evaluate with ROUGE-1/2/L and BERTScore
6. Visualize results (training curves, score distributions, ROUGE-vs-BERTScore correlation, length analysis, boxplots)
7. Qualitative inspection of best/worst summaries by ROUGE-1
8. Compare against a TextRank extractive baseline
9. Export a human evaluation template (Fluency / Adequacy / Conciseness / Faithfulness, 1–5 scale)
10. Save all predictions, metrics, and the fine-tuned model

## Project Structure

```
BanglaSum-Abstractive-Text-Summarization-for-Low-Resource-Bangla/
├── README.md                          # This file
├── banglasummarization-ab.ipynb       # Main Jupyter notebook with full pipeline
├── predictions.csv                    # Model predictions with ROUGE/BERTScore metrics
├── model_comparison.csv               # Comparison between fine-tuned model and TextRank baseline
└── human_evaluation_form.csv          # Template for manual evaluation (20 samples)
```

### Files Description

- **banglasummarization-ab.ipynb**: Complete end-to-end pipeline including data loading, preprocessing, model fine-tuning, evaluation, and visualization
- **predictions.csv**: Generated summaries with automatic metrics (ROUGE-1/2/L, BERTScore F1, generated/reference lengths) for all 200 test articles
- **model_comparison.csv**: Side-by-side comparison of our fine-tuned mT5 model vs. TextRank extractive baseline on 50 samples
- **human_evaluation_form.csv**: Pre-filled template with 20 samples for human evaluation on dimensions: Fluency, Adequacy, Conciseness, and Faithfulness (1–5 scale)

## Key Features

- **Multilingual mT5**: Leverages pre-trained multilingual model fine-tuned on XL-Sum
- **Comprehensive Metrics**: ROUGE scores (1, 2, L) + BERTScore for semantic similarity
- **Baseline Comparison**: TextRank extractive summarization as a baseline
- **Human Evaluation**: Templates provided for manual quality assessment
- **Full Documentation**: Jupyter notebook with detailed explanations and visualizations

## Dependencies

The notebook requires:
- `transformers` (Hugging Face)
- `datasets` (for XL-Sum)
- `rouge_score` (for ROUGE evaluation)
- `bert_score` (for BERTScore)
- `pandas`, `numpy`, `matplotlib`, `seaborn` (for analysis and visualization)

## Usage

1. Open `banglasummarization-ab.ipynb` in Jupyter or Google Colab
2. Follow the pipeline step-by-step:
   - Load and explore the Bengali XL-Sum dataset
   - Fine-tune the model or load pre-trained checkpoints
   - Generate summaries on test data
   - View automatic and qualitative results
3. Review predictions in `predictions.csv`
4. Use `human_evaluation_form.csv` for manual annotation

## Results Summary

- **Model Performance**: The fine-tuned mT5 achieves ROUGE-1 of 0.2366, BERTScore F1 of 0.7586
- **Baseline Comparison**: Outperforms TextRank extractive baseline (ROUGE-1: 0.24 vs 0.0)
- **Length Analysis**: Generated summaries average 14.78 words vs. 21.85 for references, showing effective compression

## Author

Abu Bakar Rakib

## License

Open for educational and research purposes.
