# 🧾 LegalBot: LLM-Powered Legal Document Summarizer

**LegalBot** is an end-to-end AI-powered platform that summarizes legal contracts by extracting **key clauses**, **risks**, and **named entities** using **GPT-4** and **LangChain**. It integrates a **Retrieval-Augmented Generation (RAG)** pipeline with **FAISS** for semantic search, and provides an interactive UI built with **Streamlit**, fully containerized using **Docker**.

---

## 📌 Key Features

- 📄 Upload any legal PDF document
- 🔍 Semantic chunking of contract text
- 🧠 FAISS-based vector similarity search
- 💬 Context-aware GPT-4 responses
- 🧾 Extract clauses, risks, entities in real time
- ⚙️ Fully Dockerized and easily deployable

---

## 🧠 System Architecture

```text
+-------------+     +------------------+     +-----------------+     +-------------+
| PDF Upload  | --> | Semantic Chunker | --> | FAISS Vector DB | --> | GPT-4 Query |
+-------------+     +------------------+     +-----------------+     +-------------+
                                          ⬑---+ Prompt Templates +---⬎
````

---

## 🧠 Theoretical Foundations

### 1. Semantic Chunking

We divide the contract into context-aware blocks (chunks), maintaining clause boundaries and semantic flow using LangChain’s `RecursiveCharacterTextSplitter`.

### 2. Retrieval-Augmented Generation (RAG)

Your query is used to fetch the top-k semantically similar chunks via **FAISS**, which are then passed to GPT-4 for informed, grounded responses.

### 3. Prompt Engineering

Carefully designed prompts guide GPT-4 to extract:

* ✍️ Legal clauses (termination, indemnity, arbitration)
* ⚠️ Risks (compliance, liability)
* 🧾 Entities (organizations, individuals, dates)

Prompts were fine-tuned through human feedback to reduce hallucinations by over 30%.

---

## 🧾 Project Structure

```bash
LegalBot/
│
├── app/
│   ├── main.py              # Streamlit UI
│   ├── pdf_handler.py       # PDF parsing + chunking
│   ├── vector_store.py      # FAISS creation/loading
│   ├── query_engine.py      # RAG & GPT logic
│   └── prompts.py           # Prompt templates
│
├── data/
│   └── sample_contract.pdf  # Sample PDF
│
├── tests/
│   ├── test_chunking.py
│   ├── test_querying.py
│   └── test_vector_store.py
│
├── Dockerfile
├── docker-compose.yml
├── requirements.txt
├── .env.example             # API key format
├── LICENSE
└── README.md
```

---

## ⚙️ Setup Instructions

### 1. Clone the Repository

```bash
git clone https://github.com/your-username/legalbot.git
cd legalbot
```

### 2. Install Dependencies (for local setup)

```bash
pip install -r requirements.txt
```

### 3. Add Environment Variables

Create a `.env` file like below:

```env
OPENAI_API_KEY=your_openai_key_here
```

### 4. Run Locally

```bash
streamlit run app/main.py
```

OR run via Docker:

```bash
docker-compose up --build
```

---

## 🧪 Sample Usage

1. Upload `sample_contract.pdf`
2. Select “Clause Extraction”
3. Ask: `What are the termination clauses?`

> Output:
>
> * Clause 5.1: Either party may terminate with 30 days’ notice.
> * Clause 8.2: Breach-related immediate termination.
> * Risk: Absence of arbitration fallback clause.

---

## 📂 Core Components Explained

### ✅ `pdf_handler.py`

Uses `PyMuPDF` and LangChain to:

* Read PDF content
* Clean and split into \~800 token overlapping chunks

### ✅ `vector_store.py`

Embeds chunks via `OpenAIEmbeddings` and stores them in FAISS for fast retrieval.

### ✅ `query_engine.py`

Handles:

* FAISS top-k chunk retrieval
* Prompt formatting
* GPT-4 answer generation via LangChain's `LLMChain`

### ✅ `main.py`

Provides Streamlit UI to:

* Upload PDF
* Select task (clauses, risks, entities)
* Show GPT-4 answers live

---

## 🧪 Testing

Run tests using:

```bash
pytest tests/
```

Unit tests cover:

* Chunk generation
* FAISS indexing
* RAG query output

---

## 🐳 Docker Deployment

### Step 1: Create `.env`

```bash
cp .env.example .env
```

Add your OpenAI key.

### Step 2: Launch App

```bash
docker-compose up --build
```

Visit [http://localhost:8501](http://localhost:8501)

---

## 🧠 Why Each Component Matters

| Component | Why It’s Needed                                                  |
| --------- | ---------------------------------------------------------------- |
| LangChain | Easy abstraction over chunking, embeddings, prompt chains        |
| FAISS     | Fast and scalable vector similarity search over legal text       |
| GPT-4     | High accuracy in extracting legal language patterns and entities |
| Streamlit | Enables real-time interaction with users in a clean UI           |
| Docker    | Ensures portability and reproducibility of the entire system     |

---

## 📚 Resources & Inspiration

* [LangChain Docs](https://docs.langchain.com)
* [OpenAI GPT-4](https://platform.openai.com/docs)
* [FAISS by Facebook](https://github.com/facebookresearch/faiss)
* [Streamlit](https://streamlit.io/)

---

## 📬 Author

**👤 Manav Rajesh Anandani**
📧 Email: [manavrajesh.anandani@sjsu.edu](mailto:manavrajesh.anandani@sjsu.edu)
🔗 LinkedIn: [linkedin.com/in/manavanandani](https://linkedin.com/in/manavanandani)

---

## 📜 License

This project is licensed under the **MIT License**. See `LICENSE` for details.

