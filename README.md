## 🩺 Health Misinformation Detection Using NLP

<div align="center">

An end-to-end NLP classification system that preprocesses health-related text, vectorizes it with TF-IDF, and trains a Logistic Regression classifier to distinguish Factual from Misinformation content with full evaluation metrics, explainability visualizations, and saved models ready for inference.

</div>

📌 Problem

Health misinformation has become one of the most pressing challenges in digital healthcare. Misleading medical advice and false health claims spread rapidly across social media, blogs, forums, and messaging platforms influencing public behavior and eroding trust in evidence-based medicine.

Manual fact-checking cannot scale to the volume of health content produced daily. This creates a critical need for automated, ML-powered solutions that can:


Flag dangerous misinformation before it reaches vulnerable populations
Support public health surveillance by detecting false claim patterns at scale
Assist medical fact-checkers with prioritized review queues
Protect platform integrity through intelligent content moderation


This project builds a complete NLP pipeline that answers the core question: Can a machine learning model reliably distinguish factual health statements from misinformation?


🎯 Objectives


Detect health misinformation in raw, unstructured textual content
Clean and normalize text through a reproducible preprocessing pipeline
Convert text into numerical representations using TF-IDF vectorization
Train a supervised Logistic Regression classifier within a Scikit-learn Pipeline
Evaluate model performance using accuracy, precision, recall, F1-score, ROC-AUC, and confusion matrix
Generate publication-ready visualizations for portfolio and research communication
Save trained models and vectorizer as .pkl files for future inference without retraining



🗂️ Dataset

The project uses a synthetic dataset representing realistic health-related textual content drawn from a range of online information sources.

Dataset Features

FeatureDescriptionidRecord identifiertextHealth-related statement or claimsource_typeType of information source (social media, blog, etc.)topicMedical topic areacontains_claimWhether the text makes an explicit health claimsentimentSentiment score of the textlabelTarget variable — 0 = Factual, 1 = MisinformationconfidenceConfidence score associated with the label


🛠️ Tools & Technologies


Language: Python 3.9+
ML Framework: Scikit-learn (Logistic Regression, Pipeline, TF-IDF)
Data Processing: Pandas, NumPy
Visualisation: Matplotlib
Model Persistence: Joblib
Data Format: OpenPyXL (.xlsx ingestion)



⚙️ Methodology / Project Workflow


Data Ingestion: Load the synthetic Excel dataset using Pandas and OpenPyXL; inspect shape, dtypes, label balance, and source distribution
Text Preprocessing: Apply a custom cleaning pipeline — lowercase conversion, URL removal, username stripping, hashtag removal, number removal, punctuation removal, and whitespace normalization
Feature Engineering: Vectorize cleaned text using TfidfVectorizer with configurable max_features, capturing term frequency weighted by inverse document frequency across the corpus
Train/Test Split: Split data into 80% training and 20% test sets with stratification to preserve class balance across both partitions
Pipeline Construction: Wrap TfidfVectorizer + LogisticRegression in a Scikit-learn Pipeline for reproducibility and deployment-ready packaging
Model Training: Fit the pipeline on training text; Logistic Regression solves a binary classification problem over TF-IDF feature space
Evaluation: Compute accuracy, precision, recall, F1-score (per class and macro-averaged), ROC-AUC, and confusion matrix on the held-out test set
Explainability: Extract and visualize the top TF-IDF features with highest positive and negative log-odds coefficients — revealing which words most strongly predict each class
Persistence: Save the fitted pipeline (model + vectorizer) as .pkl files via Joblib; verify load-and-predict integrity
Visualisation: Generate 5 output charts — label distribution, source distribution, confusion matrix, ROC curve, and top predictive words — saved to outputs/
Inference: Demonstrate real-world prediction on new text samples with class label and confidence score



📊 Key Features


✅ Complete NLP pipeline: Raw text in → cleaned → TF-IDF vectorized → classified → evaluated, all in a single reproducible script
✅ Scikit-learn Pipeline: TfidfVectorizer and LogisticRegression packaged together — prevents leakage, enables single-call .predict() on raw text at inference time
✅ Custom text preprocessor: 8-step cleaning function handles URLs, usernames, hashtags, numbers, punctuation, and whitespace — normalizes text before any modeling
✅ Stratified train/test split: Class proportions preserved across train and test partitions — essential for imbalanced health text datasets
✅ Full evaluation suite: Accuracy, precision, recall, F1-score, ROC-AUC, and confusion matrix computed and printed as a formatted classification report
✅ Coefficient-based explainability: Top TF-IDF terms ranked by Logistic Regression log-odds coefficients — shows exactly which words drive Factual vs Misinformation predictions
✅ 5 publication-ready visualisations: Label distribution, source distribution, confusion matrix, ROC curve, and top predictive words
✅ Saved model artifacts: Both the fitted model and vectorizer persisted as .pkl files — reusable for inference without retraining



📸 Visualisations

🔹 Label Distribution


Class balance across the dataset — confirms whether the binary classification problem is balanced or requires resampling strategies



Show Image


🔹 Source Distribution


Breakdown of health content by source type (social media, blog, forum, etc.) — reveals which platforms contribute most to the misinformation corpus



Show Image


🔹 Confusion Matrix


True positives, false positives, true negatives, and false negatives on the held-out test set — shows where the model succeeds and where it misclassifies



Show Image


🔹 ROC Curve


Receiver Operating Characteristic curve plotting true positive rate against false positive rate across classification thresholds — AUC quantifies overall discriminative power



Show Image


🔹 Top Predictive Words


Highest-coefficient TF-IDF terms for each class — exposes the vocabulary the model associates with factual vs misleading health content



Show Image


💬 Example Predictions

Example 1

Input:

COVID vaccines contain tracking microchips.

Output:

Prediction : Misinformation
Confidence : 0.98


Example 2

Input:

Regular exercise improves heart health.

Output:

Prediction : Factual
Confidence : 0.96


📁 Project Structure

Health-Misinformation-Detection-Using-NLP/
│
├── 📂 data/
│   └── Health_Misinformation_Detection_Using_NLP_Synthetic_Dataset.xlsx
│
├── 📂 models/
│   ├── misinformation_model.pkl        # Fitted Logistic Regression pipeline
│   └── tfidf_vectorizer.pkl            # Fitted TF-IDF vectorizer
│
├── 📂 outputs/
│   ├── label_distribution.png          # Class balance chart
│   ├── source_distribution.png         # Source type breakdown
│   ├── confusion_matrix.png            # Test set confusion matrix
│   ├── roc_curve.png                   # ROC-AUC curve
│   └── top_words.png                   # Top TF-IDF features by coefficient
│
├── health_misinformation_detection.py  # ⭐ Full pipeline — run everything
├── requirements.txt                    # Python dependencies
└── README.md


▶️ How to Run

Prerequisites

bash# Python 3.9+
# Anaconda (recommended) or virtual environment

# Clone the repository
git clone https://github.com/yourusername/Health-Misinformation-Detection-Using-NLP.git
cd Health-Misinformation-Detection-Using-NLP

# Install dependencies
pip install -r requirements.txt

Run the Full Pipeline

bashpython health_misinformation_detection.py

The script automatically:


Loads and inspects the dataset
Cleans and preprocesses all text
Vectorizes with TF-IDF and splits into train/test
Trains the Logistic Regression pipeline
Evaluates and prints the classification report
Saves the model and vectorizer to models/
Generates and saves all 5 visualizations to outputs/
Runs predictions on example new text samples


Pipeline Outputs

StageOutputLocationPreprocessingCleaned text columnIn-memory DataFrameVectorizationTF-IDF feature matrixIn-memory (train/test splits)TrainingFitted pipelinemodels/misinformation_model.pklVectorizerFitted TF-IDFmodels/tfidf_vectorizer.pklEvaluationClassification reportTerminal outputVisualisation5 chart filesoutputs/


⚠️ Limitations & Future Work

Current Limitations:


The model uses a synthetic dataset — real-world performance on live social media text may differ due to informal language, sarcasm, and evolving misinformation patterns
TF-IDF + Logistic Regression captures word frequency but not context, word order, or semantic meaning — a transformer-based model would significantly improve nuanced detection
No cross-validation is applied; a single train/test split may not fully represent model stability across different data partitions
The current pipeline does not handle multilingual content — health misinformation is a global problem requiring multilingual NLP solutions
Explainability is limited to coefficient inspection; SHAP values would provide more granular, instance-level explanations


### Future Improvements:


🤖 Fine-tune BERT, RoBERTa, or BioBERT for context-aware health misinformation classification
🌍 Add multilingual classification support using multilingual transformer models
🔍 Integrate SHAP and LIME for instance-level explainability and model transparency
📰 Extend scope to fake news detection and medical named entity recognition (NER)
📊 Build a Streamlit dashboard for interactive prediction with real-time text input
🚀 Deploy as a FastAPI REST API with Docker containerization for production use
☁️ Deploy to AWS / Azure / GCP for scalable cloud inference
📈 Add word cloud, interactive topic distribution, TF-IDF heatmaps, and precision-recall curves to the visualization suite



<div align="center">
👤 Author

**Buka Jonah**

🤖 Data Scientist | Machine Learning Enthusiast | NLP Practitioner | Public Health Analytics

Building practical AI and machine learning solutions that address real-world healthcare challenges through data-driven insights.


</div>

📄 License

This project is licensed under the MIT License free to use, adapt, and build upon for research, education, and public health applications.
See the LICENSE file for full details.


🙌 Acknowledgements


**Scikit-learn community:** for the consistent, well-documented ML API powering the classification pipeline and TF-IDF vectorization
**Pandas & NumPy:** for robust data manipulation and numerical computation throughout the preprocessing and evaluation stages
**Matplotlib:** for clean, publication-ready visualizations generated from model outputs
**Joblib:** for efficient model serialization enabling inference without retraining
**The broader NLP and Public Health AI research community:** for advancing the science of automated misinformation detection



<div align="center">
⭐ If this project helped you, please consider starring the repo!

Part of a broader portfolio of Data Science and Machine Learning projects focused on real-world public health applications.

🔗 View All Projects · Connect on LinkedIn

</div>
