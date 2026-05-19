# 🛡️ Intrusion Detection System (IDS) - CICIDS2017
A comprehensive machine learning and deep learning pipeline for network intrusion detection, built on the CICIDS2017 dataset. This project implements a two-stage classification strategy (Binary & Multi-Class) to distinguish benign traffic from malicious attacks and identify specific attack vectors.

## 📋 Overview
Network intrusion detection is critical for modern cybersecurity. This project addresses key challenges in IDS development, primarily **severe class imbalance** and **high-dimensional feature spaces**. By combining traditional ML models (Logistic Regression, Random Forest, XGBoost) with custom Deep Learning architectures (MLPs), this project evaluates performance across multiple dimensions: accuracy, precision/recall, false alarm rates, attack miss rates, and inference latency.

## 🛠️ Technologies & Libraries
- **Language:** Python 3.11+
- **Data Processing:** `pandas`, `numpy`
- **Visualization:** `matplotlib`, `seaborn`
- **Machine Learning:** `scikit-learn` (v1.2.2), `xgboost`, `imbalanced-learn` (v0.9.1 for SMOTE)
- **Deep Learning:** `tensorflow`, `keras`
- **Environment:** Jupyter Notebook / Kaggle Kernel (GPU Acceleration: NVIDIA Tesla T4)

## ✨ Key Features
- **Two-Stage Classification Pipeline:**
  - 🔹 **Binary:** Benign vs. Any Attack
  - 🔹 **Multi-Class:** Specific attack type identification (DDoS, Port Scan, Bruteforce, Web Attacks, etc.)
- **Robust Preprocessing:** Handles `inf`/`NaN` values, removes duplicates, applies `LabelEncoder`, and scales features using `MinMaxScaler`.
- **Intelligent Feature Selection:** Uses XGBoost feature importance + `SelectFromModel` (median threshold) to reduce dimensionality, followed by correlation analysis to drop highly correlated/redundant features.
- **Class Imbalance Handling:** Implements SMOTE (Synthetic Minority Over-sampling Technique) to balance training data while strictly preserving the original distribution in validation/test sets.
- **Custom Deep Learning Architectures:** 5 distinct MLP configurations per task, experimenting with layer widths, activation functions (`tanh`, `selu`), and weight initializers (`GlorotUniform`, `HeUniform`).
- **Advanced Training Controls:** `EarlyStopping`, `ReduceLROnPlateau`, and stratified 5-fold cross-validation.
- **Cybersecurity-Specific Evaluation Metrics:** Goes beyond standard accuracy to report:
  - `FAR` (False Alarm Ratio)
  - `AMR` (Attack Miss Ratio)
  - Inference Latency (ms/sample)
  - Detailed Classification Reports & Confusion Matrices

## 🚀 What You Can Do
- ✅ Run the complete end-to-end IDS pipeline from raw data loading to final model evaluation.
- ✅ Compare traditional ML models against custom Deep Learning architectures.
- ✅ Visualize data distributions, feature correlations, training histories, and confusion matrices.
- ✅ Experiment with different model architectures, feature subsets, or resampling techniques.
- ✅ Evaluate model suitability for real-time deployment using latency, FAR, and AMR metrics.
- ✅ Use the provided evaluation functions (`evaluate_b`, `evaluate_m`, `far_amr_b`, `far_amr_m`) to quickly benchmark new models.

## 📥 How to Run

### 1. Clone & Setup Environment
```bash
git clone <your-repo-url>
cd <repo-directory>
```
 Install dependencies (exact versions used in the project)
```bash
pip install pandas numpy matplotlib seaborn scikit-learn==1.2.2 imbalanced-learn==0.9.1 xgboost tensorflow
```
### 2. Prepare the Data
Download the CICIDS2017 dataset. Preprocessed .parquet files are highly recommended for faster loading.
Update the file paths in Section 1: Data Preparation to match your local directory.
(Note: The original notebook uses Kaggle paths: /kaggle/input/cicids2017/)
### 3. Execute the Notebook
Open cicids2017-deep-learning.ipynb in Jupyter Lab, VS Code, or Kaggle.
Run all cells sequentially from top to bottom. GPU acceleration is recommended for the Deep Learning training sections.
All outputs (metrics, plots, evaluations) will render inline.
🔮 Future Development & Extensions
🎛️ Hyperparameter Tuning: Integrate Optuna or scikit-learn's RandomizedSearchCV for automated architecture and parameter optimization.
🌊 Sequence Modeling: Upgrade to LSTM/GRU or Transformer architectures to capture temporal dependencies in network traffic flows.
⏱️ Time-Series Splitting: Replace random train_test_split with chronological/time-based splits to better simulate real-world deployment and prevent temporal data leakage.
🚀 Production Deployment: Wrap the best-performing model in a FastAPI or Streamlit microservice for real-time packet/flow analysis.
🛡️ Adversarial Testing: Evaluate model resilience against adversarial network traffic evasion techniques.
## 💡 What I Learned
Accuracy is Deceptive in Security: High overall accuracy often masks poor minority-class performance. Metrics like F1-Score, FAR, and AMR are essential for evaluating real-world security effectiveness.
Feature Engineering > Model Complexity: Proper feature selection and correlation filtering significantly reduced training time, mitigated overfitting, and often outperformed blindly adding more neural network layers.
ML vs DL Trade-offs for Tabular Data: While custom MLPs can achieve competitive accuracy, tree-based models (XGBoost, Random Forest) generally offer faster inference, better out-of-the-box performance, and higher interpretability for structured network flow data.
Pipeline Hygiene is Crucial: Fitting scalers and applying SMOTE strictly on the training split is mandatory. Applying them before splitting causes severe data leakage and inflated validation scores.
Domain-Specific Evaluation Matters: Understanding and implementing cybersecurity metrics (FAR/AMR) transforms a generic classification project into a practical security tool. A model with 99% accuracy but a high AMR is dangerous in production.
## 📝 Note: This project is designed for educational and research purposes. Always validate IDS models against modern, up-to-date threat landscapes and real network traffic before production deployment.
