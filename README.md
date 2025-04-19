# Log Classification System

## 📋 Overview

A hybrid **Log Classification System** designed for a US-based client at ATCK Technologies. This solution automates log monitoring by combining rule‑based, machine‑learning, and LLM‑driven approaches to accurately categorize incoming logs in real time, reducing downtime, manual effort, and security risks.

## ✨ Features

- **Regex‑Based Classification**  
  Quickly detect and label logs matching fixed patterns via Python regular expressions.  
- **BERT + Logistic Regression**  
  Leverage BERT embeddings with a lightweight PyTorch logistic regression layer for patterns with ample training data.  
- **LLM‑Fallback Classification**  
  Employ a Large Language Model (e.g., LLaMA) when training samples are scarce or patterns are too complex.  
- **FastAPI Backend**  
  Serve classification endpoints over a high‑performance REST API.  
- **Extensible & Configurable**  
  Easily add new regex rules, retrain BERT models, or swap in different LLMs with minimal code changes.  
- **Real‑Time Monitoring**  
  Aggregate and classify logs on the fly for immediate alerting and dashboard integration.

## 🔧 Technical Stack

- **Deep Learning & NLP**  
  - BERT (via Hugging Face Transformers)  
  - LLaMA or alternative LLM  
  - PyTorch for embedding & logistic regression  
- **Rule‑Based**  
  - Python `re` module for regular expressions  
- **API Layer**  
  - FastAPI with Uvicorn  
- **Development Environment**  
  - PyCharm Professional (3‑month free trial available)  
- **Data Handling & Clustering**  
  - Pandas, NumPy  
  - scikit‑learn’s DBSCAN for pattern discovery  

## 🚀 Getting Started

### 1. Clone the Repo  
```bash
git clone https://github.com/yourusername/log-classification-system.git
cd log-classification-system
```

### 2. Create & Activate Virtual Env  
```bash
python3 -m venv venv
source venv/bin/activate
```

### 3. Install Dependencies  
```bash
pip install -r requirements.txt
```

### 4. Prepare Data  
- Place your log files (CSV/Excel) into `data/`  
- Ensure columns: `timestamp`, `source`, `message`, `target_label`  

### 5. Index Regex Patterns  
```bash
python scripts/cluster_and_generate_regex.py   --input data/raw_logs.xlsx   --output configs/regex_patterns.json
```

## 🖥️ How to Use

1. **Run the Classifier**  
   ```bash
   uvicorn app.main:app --reload
   ```
2. **Upload & Classify Logs**  
   - POST your log batch to `/classify/batch`  
   - GET classification results at `/classify/{log_id}`  
3. **Monitor in Real Time**  
   - Connect to WebSocket `/ws/logs` for continuous stream  

## 🧠 How It Works

1. **Log Ingestion**  
   Logs are received in CSV/Excel and parsed into a DataFrame.  
2. **Pattern Discovery**  
   DBSCAN clustering identifies recurring message structures to seed regex rules.  
3. **Hybrid Classification Pipeline**  
   - **Step 1: Regex Engine**  
     Match against predefined patterns for deterministic categories.  
   - **Step 2: BERT Model**  
     For unmatched logs with ≥N samples, encode with BERT and classify via logistic regression.  
   - **Step 3: LLM Fallback**  
     For outliers or under‑sampled categories, query the LLM with a prompt template for final labeling.  
4. **Result Aggregation**  
   Responses from each stage are merged, with confidence scores, and stored in the metadata index.

## 📁 Project Structure

```
log-classification-system/
├── models/
│   └── log_classifier.joblib       # Trained BERT+LR model
├── training/
│   ├── dataset/                    # Raw and labeled log files
│   └── training.ipynb              # Exploration & prototyping notebook
├── classify.py                     # CLI for single/batch classification
├── main.py                         # Entry point for model training & utils
├── processor_bert.py               # BERT embedding & LR classification
├── processor_llm.py                # LLM‐based classification logic
├── processor_regex.py              # Regex pattern generation & matching
├── server.py                       # FastAPI application
├── configs/                        # Configuration files (e.g. regex patterns)
├── requirements.txt
└── LICENSE                         # MIT License
```

## 🛠️ Customization

- **Add New Regex Rules**  
  Update `configs/regex_patterns.json` or rerun the clustering script with new data.  
- **Retrain BERT Model**  
  Modify `models/bert_classifier.py` to tweak hyperparameters or swap in a different transformer.  
- **Swap LLM**  
  In `models/llm_classifier.py`, change the model endpoint or prompt template to use GPT‑4, LLaMA, etc.  

## 📊 Performance Considerations

- **Batch Inference**  
  Group log entries to amortize model loading overhead.  
- **GPU Acceleration**  
  Use a CUDA‑enabled machine for BERT embedding and LLM calls.  
- **Caching & Async I/O**  
  Leverage FastAPI’s async features and an in‑memory cache for repeated queries.  
- **Scalability**  
  Deploy behind a load‑balancer; consider FAAS for sporadic LLM fallback calls.

## 📝 License

This project is licensed under the **MIT License** – see the [LICENSE](LICENSE) file for details.
