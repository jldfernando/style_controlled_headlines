# Style-Controlled Headline Generation for PH News

## Overview
This project aims to fine-tune a BART model (and explore others like Flan-T5 and PEGASUS) using LoRA (Low-Rank Adaptation) to generate headlines from Philippine news snippets. The unique aspect of this project is the control over the style of the generated headline: **Neutral**, **Punchy**, or **Formal**.

## Project Structure

### Notebooks
The notebooks are designed to be run in the following order:

1.  **Data Preparation**:
    *   `00_data_cleaning.ipynb`: Initial cleaning and processing of raw data.
    *   `01_data_prep.ipynb`: Creation of synthetic data, splits, and final dataset preparation.

2.  **Training**:
    *   `02_training.ipynb`: Main training notebook for BART model (Baseline and Style-Controlled).
    *   `02_training_FlanT5.ipynb`: Training notebook for Flan-T5 model.
    *   `02_training_PEGASUS.ipynb`: Training notebook for PEGASUS model.

3.  **Evaluation**:
    *   `03_evaluation.ipynb`: Evaluation metrics (ROUGE, Style Accuracy, Factuality) for BART.
    *   `03_evaluation_FlanT5.ipynb`: Evaluation for Flan-T5.
    *   `03_evaluation_PEGASUS.ipynb`: Evaluation for PEGASUS.

### Directories
*   `data/`: Contains raw and processed datasets.
*   `output/`: Stores model checkpoints, logs, and generated results.
*   `notebooks/`: Contains the Jupyter notebooks listed above.

## Methodology Summary

### Phase 1: Data & Preprocessing
*   Collection of PH News Snippets.
*   Human annotation for Neutral, Punchy, and Formal styles.
*   Data splitting (Train/Dev/Test) and tokenization.

### Phase 2: Modeling
*   **Base Models**: BART-base (primary), Flan-T5, PEGASUS.
*   **Technique**: LoRA for efficient fine-tuning.
*   **Style Control**: Integration of special tokens (`<neutral>`, `<punchy>`, `<formal>`) to guide generation.

### Phase 3: Training
*   **Baseline**: Standard summarization (Snippet -> Headline).
*   **Style-Controlled**: Conditioned generation (`[STYLE_TOKEN] Snippet` -> Matching Headline).

### Phase 4: Evaluation
*   **ROUGE**: For content overlap.
*   **Style Accuracy**: Using an external classifier to verify style adherence.
*   **Factuality**: NLI-based consistency checking.

## Setup

1.  **Install Dependencies**:
    ```bash
    pip install -r requirements.txt
    ```

2.  **Run Notebooks**:
    Start with `00_data_cleaning.ipynb` and proceed sequentially through the numbered notebooks. Choose the specific training/evaluation notebook based on the model you wish to experiment with.