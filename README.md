# 🛡️ Network Intrusion Detection System

A machine-learning dashboard for classifying network traffic as **normal** or **potentially malicious**. The project trains a Random Forest model from a CSV dataset and presents results through an interactive Gradio interface.

> Educational project: use this as a detection aid, not as a replacement for production security controls.

## ✨ Features

- Detects normal and attack traffic from network-flow features
- Supports both numerical and categorical dataset columns
- Removes duplicate records and rows with missing labels
- Handles missing values automatically
- Uses a balanced Random Forest classifier
- Shows accuracy, precision, recall, F1 score, and a confusion matrix
- Provides histogram-based exploratory data analysis
- Saves the trained model pipeline for reuse
- Includes a synthetic demo dataset generator

## 🧰 Tech stack

| Area | Technology |
| --- | --- |
| Language | Python |
| Machine learning | scikit-learn |
| Data processing | pandas, NumPy |
| Visualization | Matplotlib |
| Dashboard | Gradio |
| Model persistence | joblib |

## 📁 Project structure

```text
network-intrusion-detection-system/
├── app.py                         # Training workflow and Gradio dashboard
├── requirements.txt               # Python dependencies
├── scripts/
│   └── generate_demo_data.py      # Creates a sample dataset
├── data/                          # Add your CSV dataset here
└── artifacts/                     # Saved trained model (created at runtime)
```

## 🚀 Getting started

### 1. Clone the repository

```bash
git clone https://github.com/YOUR-USERNAME/network-intrusion-detection-system.git
cd network-intrusion-detection-system
```

### 2. Create and activate a virtual environment

**Windows (PowerShell)**

```powershell
python -m venv .venv
.venv\Scripts\Activate.ps1
```

**macOS / Linux**

```bash
python3 -m venv .venv
source .venv/bin/activate
```

### 3. Install dependencies

```bash
pip install -r requirements.txt
```

### 4. Generate demo data (optional)

```bash
python scripts/generate_demo_data.py
```

### 5. Launch the dashboard

```bash
python app.py
```

Open the local URL displayed in the terminal, typically `http://127.0.0.1:7860`.

## 📊 Using your own dataset

Your file must be a CSV with a required `label` column. Every other column is treated as an input feature.

Example:

```csv
duration,protocol,service,src_bytes,dst_bytes,failed_logins,label
12.4,TCP,http,1810,530,0,normal
46.1,TCP,ssh,320,82,3,attack
```

Run the application against it with:

```bash
python app.py --data path/to/network_data.csv
```

The dashboard displays labels named `normal`, `benign`, `0`, or `false` as normal traffic. Other predicted labels are shown as potential attack traffic.

## 🧠 Model workflow

1. Load and validate the CSV dataset.
2. Remove duplicate rows and records without a label.
3. Split the dataset into 80% training and 20% testing data.
4. Impute missing numerical values with the median and categorical values with the most frequent value.
5. Scale numerical features and one-hot encode categorical features.
6. Train a 200-tree Random Forest classifier with balanced class weights.
7. Evaluate performance and save the complete pipeline to `artifacts/network_intrusion_model.pkl`.

## 🔒 Security notes

- Do not commit real network captures, credentials, IP addresses, or sensitive datasets.
- Validate false-positive and false-negative rates with representative traffic before deployment.
- Combine ML detections with alert review, network segmentation, logging, and incident-response procedures.

## 📄 License

This project is intended for learning and portfolio use. Add a license file before distributing it publicly.
