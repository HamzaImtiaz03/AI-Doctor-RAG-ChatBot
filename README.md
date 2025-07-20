
# 💬 Doctor: AI-Powered Medical Chatbot

**Smart, Fast, Reliable Medical Assistance at Your Fingertips**

---

## 🔍 Overview

**Doctor** is an AI-driven medical chatbot application built with Python that delivers **accurate, trustworthy, and context-aware answers** to medical questions. It uses a **Retrieval-Augmented Generation (RAG)** architecture, combining **Large Language Models (LLMs)** with **FAISS vector-based semantic search** to retrieve relevant information from a trusted medical source—**The Gale Encyclopedia of Medicine, Second Edition**.

With an intuitive **Streamlit-based user interface**, Doctor allows users to interact seamlessly and gain medical insights in real time. The application supports LLMs hosted on both **HuggingFace (paid)** and **Groq (free and ultra-fast)**, giving users deployment flexibility.

---

## ✨ Key Features

* 🔍 **Contextual Retrieval with RAG**: Integrates FAISS for embedding search and retrieval over medical encyclopedia data.
* 📚 **Trusted Medical Source**: All responses are strictly based on *The Gale Encyclopedia of Medicine, Second Edition*—a reputable medical reference.
* 🧠 **Multi-LLM Support**: Compatible with:

  * `mistralai/Mistral-7B-Instruct-v0.3` via HuggingFace (token required)
  * `meta-llama/llama-4-maverick-17b-128e-instruct` via Groq (API key required)
* 📦 **Fast & Efficient Embedding**: Uses `sentence-transformers/all-MiniLM-L6-v2` for generating compact, high-quality document embeddings.
* 💻 **Interactive UI**: Built with Streamlit for a clean, modern user experience.
* 🎯 **Focused Prompt Engineering**: Custom prompt templates ensure answers remain concise, relevant, and fact-based.
* 🧩 **Modular & Scalable Design**: Easy to extend for new datasets, LLMs, or front-end platforms.
* 🧪 **CLI Mode**: Offers a command-line interface for power users or automated workflows.
* 🧰 **Environment Isolation**: Uses `uv` for reliable virtual environment and dependency management.

---

## 🗂 Data Source

Doctor relies exclusively on **The Gale Encyclopedia of Medicine, Second Edition**, stored in the `data/` directory as a PDF. This rich medical resource covers conditions, treatments, procedures, and general health topics.

---

## ⚙️ Prerequisites

* Python ≥ 3.13
* `uv` (Universal Virtualenv + Dependency Tool)
* Environment Variables:

  * `HF_TOKEN` – for HuggingFace API access (if used)
  * `GROQ_API_KEY` – for Groq-hosted model access

---

## 📥 Installation

1. **Clone the Repository**

```bash
git clone https://github.com/HamzaImtiaz03/AI-Doctor-RAG-ChatBot
cd doctor
```

2. **Set Up Environment**

```bash
uv venv
source .venv/bin/activate   # Windows: .venv\Scripts\activate
```

3. **Install Dependencies**

```bash
uv add -r requirements.txt
```

4. **Configure Environment Variables**
   Create a `.env` file in the root directory:

```env
HF_TOKEN=your_huggingface_token
GROQ_API_KEY=your_groq_api_key
```

5. **Add the Medical PDF**
   Place `The_GALE_ENCYCLOPEDIA_of_MEDICINE_SECOND.pdf` into the `data/` folder.

---

## 🚀 Getting Started

### Step 1: Generate Vector Store

Run the script to extract, chunk, embed, and index the data:

```bash
uv run python create_memory_for_llm.py
```

* Creates 500-token chunks with 50-token overlaps.
* Stores embeddings in `vectorstore/db_faiss`.

### Step 2: Launch the Web Chatbot

```bash
streamlit run medibot.py
```

* Open `http://localhost:8501` in your browser.
* Enter medical queries (e.g., *"What are the symptoms of hypertension?"*).
* Responses are grounded in the encyclopedia and display source references.

### Step 3 (Optional): Use CLI Mode

```bash
uv run python connect_memory_with_llm.py
```

Type your query directly in the terminal and get real-time responses with citations.

---

## 📁 Project Structure

```
doctor/
├── main.py                           # Entry point script
├── medibot.py                        # Streamlit UI
├── connect_memory_with_llm.py       # CLI interface
├── create_memory_for_llm.py         # PDF → FAISS vector builder
├── data/
│   └── The_GALE_ENCYCLOPEDIA_of_MEDICINE_SECOND.pdf
├── vectorstore/
│   └── db_faiss/                     # Stores the FAISS index
├── requirements.txt                  # Python dependencies
├── pyproject.toml                    # Project metadata
└── .env                              # Environment variables (not committed)
```

---

## 📦 Dependencies

Key libraries used:

* `langchain`, `langchain-community`: Core RAG logic and integrations
* `langchain-groq`, `langchain-huggingface`: LLM connectors
* `sentence-transformers`: For generating vector embeddings
* `faiss-cpu`: Efficient vector search engine
* `pypdf`: PDF text extraction
* `streamlit`: Front-end web interface
* `uv`: Virtualenv and dependency manager

Check `requirements.txt` for the full list.

---

## 🧠 LLM & Vector Store Configuration

* **Embedding Model**: `sentence-transformers/all-MiniLM-L6-v2`
* **LLM Options**:

  * HuggingFace: `mistralai/Mistral-7B-Instruct-v0.3`
  * Groq: `meta-llama/llama-4-maverick-17b-128e-instruct`
* **FAISS Settings**:

  * Chunk Size: 500 tokens
  * Overlap: 50 tokens
  * Output Directory: `vectorstore/db_faiss/`
* **Prompt Template**: Engineered to use *only* information from the medical encyclopedia.

---

## 🛠 Troubleshooting

| Issue                        | Solution                                                            |
| ---------------------------- | ------------------------------------------------------------------- |
| ❌ Missing API Keys           | Check `.env` for correct `HF_TOKEN` and `GROQ_API_KEY`              |
| 📄 PDF Not Found             | Ensure `The_GALE_ENCYCLOPEDIA_of_MEDICINE_SECOND.pdf` is in `data/` |
| 🧠 Vector Store Errors       | Run `create_memory_for_llm.py` again to regenerate FAISS store      |
| ⚠️ Port Conflict (Streamlit) | Make sure port `8501` is available or run with `--server.port`      |
| 🐍 Python Errors             | Confirm you're using Python 3.13+ with `uv` installed               |

---

## 🤝 Contributing

Contributions are highly encouraged!

* Submit PRs for feature additions or improvements
* Open issues for bugs or enhancements
* Follow standard code practices and provide clear documentation

---

## 📄 License

Licensed under the **MIT License**. See the `LICENSE` file for full details.

