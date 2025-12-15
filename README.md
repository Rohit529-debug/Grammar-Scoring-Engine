# Grammar-Scoring-Engine
## 1. Project Overview

This repository contains an end-to-end **Grammar Scoring Engine** designed to evaluate grammatical accuracy in spoken English audio samples.  
The system takes raw speech audio as input and outputs a **continuous grammar score between 0 and 5**, aligned with the provided Likert-scale rubric.

The project was developed as part of the **SHL Research Intern Hiring Assessment (2025)** and emphasizes **interpretability, robustness, and evaluation rigor**.

---

## 2. Methodology Overview

The solution follows a modular pipeline:

### 2.1 Audio Processing
- Input audio files in WAV format (45–60 seconds duration)
- Audio loaded and resampled using `librosa` for consistency

### 2.2 Speech-to-Text Transcription
- **Whisper ASR (base model)** used to transcribe speech
- Robust to background noise, accents, and varying audio quality

### 2.3 Grammar & Linguistic Feature Extraction
Extracted **20+ interpretable features** including:

- **Basic Statistics:** Word count, sentence count, average sentence length, average word length
- **Grammar Error Metrics:** Grammar error count and normalized error rate using LanguageTool
- **Sentence Structure & Complexity:** Incomplete sentences, complex sentence rate, conjunction usage
- **Linguistic Richness:** Vocabulary richness, noun phrases, verb phrases, dependency depth
- **Speech Patterns:** Filler words, repetitions

These features closely align with the **grammar scoring rubric**.

---

## 3. Model Architecture

- **Algorithm:** XGBoost Regressor

### Rationale
- Strong performance on small structured datasets (409 samples)
- Captures non-linear relationships between linguistic features
- Built-in regularization reduces overfitting
- Provides feature importance for interpretability

---

## 4. Evaluation Strategy

- **5-Fold Cross-Validation** for robust performance estimation
- **Primary Metrics:**
  - Root Mean Squared Error (RMSE)
  - Pearson Correlation Coefficient

Notebook includes:
- Predicted vs Actual plots
- Residual analysis
- Feature importance visualization
- Error analysis across grammar score ranges

---

## 5. Repository Structure

Grammar-Scoring-Engine/
- Grammar_Scoring_Engine_SHL.ipynb    (Complete implementation and analysis)
- submission.csv                       (Final predictions on test dataset)
- README.md                            (Project documentation)



## 6. Files Description

- **Grammar_Scoring_Engine_SHL.ipynb**  
  Complete pipeline: preprocessing, transcription, feature extraction, model training, evaluation, visual analysis, and final predictions.

- **submission.csv**  
  Test dataset predictions in required submission format (`filename`, `label`).

---

## 7. Notes & Assumptions

- Audio files are not included due to size constraints
- Grammar scoring quality depends on ASR transcription accuracy
- Predictions are clipped to the valid score range `[0, 5]`

---

## 8. Limitations & Future Improvements

- **ASR Dependency:** Transcription errors may propagate to grammar features
- **Feature Expansion:** Advanced discourse-level or syntactic features could improve performance
- **Audio-Level Features:** Prosodic cues (pauses, speech rate) could be incorporated directly from audio
- **Model Ensembling:** Combining multiple regressors may further improve robustness

---

## 9. Conclusion

This project demonstrates a robust and interpretable approach to automated grammar scoring from spoken audio.  
By combining speech recognition, linguistically meaningful feature engineering, and supervised learning, the system achieves strong performance while maintaining explainability—making it suitable for educational and assessment-driven applications.
