### PHASE 1: Data & Preprocessing (Focus: Dataset Quality)
1. **Data Acquisition:** Collect 300-400 PH News Snippets.
2. **Human Annotation:** Write 3 headline variants per snippet: Neutral, Punchy, Formal.
3. **Dataset Formalization:** Create final JSONL/CSV file (One row per story, 3 headline fields).
4. **Data Split:** Apply Story-level Train (70%) / Dev (15%) / Test (15%) split.
5. **Tokenization:** Tokenize inputs and targets, applying max length limits (e.g., Snippet <256, Headline <64).

### PHASE 2: Modeling Setup (Focus: Efficient Fine-tuning)
1. **Base Model Selection:** Select summarization-style Encoder-Decoder (e.g., BART-base).
2. **Style Token Integration:** Add and initialize **<neutral>, <punchy>, <formal>** to the tokenizer and model embeddings.
3. **LoRA Configuration:** Initialize PEFT (LoRA/QLoRA) config with specific rank (e.g., r=8 or 16).

### PHASE 3: Training Runs (Focus: Fair Comparison)
1. **Baseline Training:** Fine-tune LoRA adapter on (Snippet -> Generic Headline).
2. **Style-Controlled Training:** Fine-tune LoRA adapter on ([STYLE\_TOKEN] Snippet -> Matching Headline).
3. **Reproducibility Log:** Fix random seeds; Log all configs (Hyperparameters, LoRA settings, Model).

### PHASE 4: Comprehensive Evaluation (Focus: Publishable Metrics)
1. **Content (ROUGE):** Calculate ROUGE-1/L on generated vs. reference headlines (Overall & Per-Style).
2. **Style Accuracy:** Train external Style Classifier; Use it to check if generated headline style matches requested token.
3. **Factuality (NLI):** Use NLI Model to check (Snippet as Premise $\rightarrow$ Headline as Hypothesis) for Entailment.
4. **Final Analysis:** Generate comparison plots: Baseline vs. Style-Controlled (ROUGE, Factuality) and Per-Style Performance.