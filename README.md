
# Talk2Data (Anonymous ICDM-25 BIGIS Workshop Submission)

> **Status:** Public, anonymised artifact for peer-review supporting the IEEE ICDM 2025 BIGIS Workshop paper *“A Multimodal Conversational Agent for Tabular Data Analysis”.*  All identifying metadata has been removed; the canonical repository URL will change if the paper is accepted.

https://github.com/user-attachments/assets/ea975371-53bd-4d99-952b-7a86bcf71381

---


## ✨ What is Talk2Data?

Talk2Data is an end‑to‑end **voice → code → visual + speech** agent that lets anyone explore tabular datasets conversationally.  It combines:

* **ASR** (OpenAI Whisper) to transcribe user speech.
* **LangGraph‑routed LLM** (Qwen‑2.5‑Coder) that decides whether to answer directly or generate Python.
* **Secure sandbox** that executes LLM‑generated Pandas / Matplotlib code with zero network / FS writes.
* **TTS** (Coqui VITS) so the agent can read results aloud.
* **Memory** to support multi‑turn follow‑ups like “Now colour by gender”.

While our evaluation uses public benchmarks, the framework is designed to generalize to intelligence and security contexts where analysts need rapid, conversational access to large structured datasets.

A 1‑min demo video (📽 `demo.mp4`) shows the full workflow.

---

## 🗂 Repository layout

```
.
├── talk2data-django/      # Django sandbox execution + memory management + UI
├── talk2data-fastAPI/     # FastAPI service running ASR, LLM, TTS
├── demo.mp4               # 1-min demo.
├── LICENSE                # Apache‑2.0
└── README.md              # You are here
```

---

## 🚀 Quick start (local)

```bash
# Clone anonymously
git clone https://github.com/ml-dev-anonymous/talk2data.git && cd talk2data

# Set up Python 3.10 virtual‑env
python -m venv .venv && source .venv/bin/activate

# Install deps (split by component)
pip install -r talk2data-django/requirements.txt
pip install -r talk2data-fastAPI/requirements.txt

# 1️⃣  Launch backend API (port 6000)
cd talk2data-fastAPI
CUDA_VISIBLE_DEVICES=0 uvicorn api:app --host 0.0.0.0 --port 6000 &

# 2️⃣  In a new shell, launch the Django UI (port 6001)
cd ../talk2data-django
python manage.py runserver

# Open http://localhost:6001 in your browser and start chatting.
```

## 📥 Datasets

We evaluate on three publicly available tabular datasets (not included in the repo). but below are the Kaggle links to the datasets:

```bash
# Otto Group Product Classification (≈ 27 MB)
[kaggle competitions download -c otto-group-product-classification-challenge -p data/otto && unzip data/otto/*.zip -d talk2data-fastAPI/evaluation_benchmark
](https://www.kaggle.com/competitions/otto-group-product-classification-challenge/data)

# US Flights 2008 (≈ 673 MB)
[kaggle datasets download -d vikalpdongre/us-flights-data-2008 -p data/flights2008 && unzip data/flights2008/*.zip -d talk2data-fastAPI/evaluation_benchmark
](https://www.kaggle.com/datasets/vikalpdongre/us-flights-data-2008)

# Students Performance in Exams (≈ 70 KB)
[kaggle datasets download -d spscientist/students-performance-in-exams -p data/students && unzip data/students/*.zip -d talk2data-fastAPI/evaluation_benchmark
](https://www.kaggle.com/datasets/spscientist/students-performance-in-exams)
```

And for each dataset we created 16 natural language commands, a total of 48 commands can be found under `talk2data-fastAPI/evaluation_benchmark`.

---

## 📊 Reproducing paper benchmarks

The code to run the evaluation is `talk2data-fastAPI/experiment.py`, it will generate the output inside `talk2data-fastAPI/evaluation_results` along with all metrics.

---

## 📝 Citation

```bibtex
@misc{talk2data2025anonymous,
  title        = {A Multimodal Conversational Agent for Tabular Data Analysis},
  howpublished = {Anonymous GitHub repository},
  note         = {IEEE ICDM 2025 BIGIS Workshop under review},
  year         = {2025}
}
```

---

## 🔐 License

Apache License 2.0 — see `LICENSE`.  Demo datasets retain their original Kaggle licences.

---

## 💬 Questions?

Open an issue. We monitor the repo during the review period while maintaining anonymity.
