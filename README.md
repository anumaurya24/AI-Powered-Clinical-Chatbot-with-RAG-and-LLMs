
# 🛡️ **SafeGuardian Pro – AI-Powered Clinical Safety Chatbot (RAG + LLMs)**

**Python • FastAPI • HuggingFace Transformers • RAG • Triage Rules • SQLite • Embeddings**

SafeGuardian Pro is a modular, safety-focused healthcare assistant designed to classify sensitive user inputs, validate intent, detect red-flag symptoms, and provide medically safe responses using a combination of **LLM-based understanding**, **retrieval-augmented generation (RAG)**, and a **clinical triage rule engine**.

This project demonstrates end-to-end design of a **real-world safety-critical chatbot**, including preprocessing, retrieval, inference orchestration, and secure response generation.

---

## 🚀 **Key Features**

### 🧠 **1. Transformer-Based Clinical Intent Understanding**

* Uses pre-trained HuggingFace transformer models to extract embeddings
* Classifies user messages into categories (symptom reporting, medical queries, unsafe content, general conversation)
* Extracts medical signals (symptom, duration, severity)

---

### 🔍 **2. Retrieval-Augmented Generation (RAG)**

* Local medical knowledge base stored in SQLite / JSON
* Embeddings + cosine similarity to fetch the safest clinical context
* Ensures LLM answers remain grounded and medically factual
* Avoids hallucinations

---

### 🚨 **3. Red-Flag Detection + Triage Rules Engine**

A core safety component that flags:

* Chest pain
* Shortness of breath
* Sudden confusion
* Bleeding
* Seizure-like episodes
* Self-harm or violence

Returns emergency instructions immediately if thresholds are met.

---

### 🏗️ **4. Modular Backend Architecture (FastAPI)**

Separation of concerns:

```
backend/
│── main.py                # API router
│── embeddings.py          # Embedding generator
│── retriever.py           # Medical RAG retriever
│── triage_engine.py       # Clinical rules engine
│── classifier.py          # Text categorization
│── database.py            # Local knowledge store
│── models/                # LLM & embedding models
│── utils/                 # Logging, cleanup, validators
```

This modularity allows replacing parts independently (e.g., plug in a faster embedding model or GPU-accelerated inference engine).

---

### 🔒 **5. Safety-First Response Generator**

Pipeline:

1. Classify the message
2. Run red-flag triage rules
3. Retrieve medical context (RAG)
4. Generate structured output
5. Force safe-response templates for dangerous situations

Ensures no misleading or harmful clinical advice.

---

### 📊 **6. Logging & Monitoring Ready**

Designed to capture:

* Message risk category
* Model confidence
* Retrieval scores
* Triage decision path

Can be integrated with Azure/GCP logs for scaling.

---

## 🩺 **Why SafeGuardian Pro Is Relevant to Dell OCTO**

Dell focuses on **efficient inference, modular ML design, and safety in AI pipelines**.

SafeGuardian Pro demonstrates:

✔ **Inference orchestration logic**
✔ **Embedding + retrieval performance considerations**
✔ **Model abstraction layers (LLM swap-ready)**
✔ **Rule-based + ML hybrid decision systems**
✔ **Scalable FastAPI microservice structure**
✔ **Modular GPU-ready components**

This is exactly what Dell OCTO looks for in research interns.

---

## 📂 **Project Structure**

```
safeguardian_pro/
│
├── backend/
│   ├── main.py
│   ├── embeddings.py
│   ├── retriever.py
│   ├── classifier.py
│   ├── triage_engine.py
│   ├── database.py
│   ├── utils/
│   └── models/
│
├── knowledge_base/
│   ├── symptoms.json
│   └── emergency_rules.json
│
├── tests/
│   ├── test_triage.py
│   ├── test_retriever.py
│   └── test_classifier.py
│
├── requirements.txt
├── README.md
└── safeguaridan_pro.ipynb   # Exploratory notebook
```

---

## 🧪 **How to Run Locally**

### Install dependencies

```bash
pip install -r requirements.txt
```

### Run the API

```bash
uvicorn backend.main:app --reload
```

Swagger docs appear at:
👉 [http://127.0.0.1:8000/docs](http://127.0.0.1:8000/docs)

---

## 📘 **Example API Request**

### **POST /analyze**

```json
{
  "message": "I have sharp chest pain for the last 20 minutes"
}
```

### **Response**

```json
{
  "category": "symptom",
  "severity": "high",
  "triage": "EMERGENCY",
  "instruction": "Please call emergency services immediately.",
  "retrieved_context": ["chest pain key facts..."],
  "safe_response": "This symptom requires urgent clinical attention."
}
```

---

## 📈 **Future Improvements**

* GPU-accelerated embedding + generation
* Replace transformers with high-throughput inference engines (vLLM / TensorRT-LLM)
* Add multimodal inputs (voice symptom reporting)
* Expand medical knowledge base
* Add LangChain for chain-of-thought reasoning

---
