# 📞 Multi-Source Telecom RAG Chatbot

An enterprise-grade Retrieval-Augmented Generation (RAG) system built with Python, LangChain, and ChromaDB. This customer care assistant dynamically references three distinct knowledge facets—unstructured engineering guides, structured FAQ files, and historical relational tickets—to provide grounded, hallucination-free answers to critical inquiries such as troubleshooting slow connectivity, billing autopay setups, and resolving call drops.

## 🏗️ System Architecture Blueprint

Below is the conceptual layout of the platform's multi-source processing and deterministic generation cycle:

![System Architecture Blueprint](image_M4rByH.png)

---

## 📖 Project Overview

Modern customer support demands real-time responses grounded in verified data across scattered data formats. This application acts as a production-style blueprint for resolving telecom support issues efficiently. Rather than relying on a single knowledge vector space, the backend dynamically processes three different structural inputs simultaneously:

1. **Relational Support Tickets (`tickets.db`):** An operational SQLite instance containing historic customer issues, long descriptions, and accurate engineering resolutions. Historic resolutions act as a reference base to solve newly submitted customer complaints deterministically.
2. **Structured FAQ Sheets (`faq.csv`):** Pre-compiled question-and-answer pairs capturing highly repetitive operational parameters (e.g., balance check short-codes or billing portal details).
3. **Unstructured Reference Guides (`telecom_guide.pdf`):** Multi-page PDF literature containing deep technical infrastructure documentation.

### Core Processing Mechanics
* **Semantic Indexing:** Documents are vectorized using `sentence-transformers/all-MiniLM-L6-v2`. Small, naturally atomic pieces (FAQs and database records) are processed as independent standalone chunks, whereas long documentation PDFs are divided using a recursive chunk size of 600 characters with a 100-character context continuity overlap.
* **Isolated Multi-Collection Aggregation:** ChromaDB acts as the persistent storage engine, managing three separate vector tables. The custom orchestration architecture concurrently fetches top-K semantic results from all collections to provide complete contextual grounding.
* **Grounded Generation Output:** Compiled string pipelines feed directly into LangChain Expression Language (LCEL) runtime chains. If data cannot be surfaced across the retrieval grid, strict system boundaries instruct the underlying model to transparently state it lacks the context rather than fabricating responses.

---

## 📂 Repository Structure

```text
telecom_chatbot/
│
├── data/
│   ├── telecom_guide.pdf     # Unstructured engineering guidelines
│   ├── faq.csv               # Pre-compiled business question matrix
│   └── tickets.db            # SQLite instance detailing historic support tickets
│
├── chroma_store/             # Local database directory caching persistent vectors
├── ingest_pdf.py             # Recursively splits and encodes technical literature
├── ingest_faq.py             # Maps CSV rows straight into isolated vector blocks
├── ingest_tickets.py         # Transforms SQLite history columns to database vectors
├── retriever.py              # Multi-channel top-K context crawler API
├── rag_chain.py              # Compiles LCEL blocks (Prompt -> LLM -> Parser)
├── app.py                    # Graphical frontend interface powered by Streamlit
└── .env.sample               # Environment token tracking blueprint
```

## 🛠️ Technology Stack

* **RAG Framework:** LangChain / LCEL (LangChain Expression Language)
* **Vector Store:** ChromaDB (Isolated Multi-Collection Indexing)
* **Embedding Model:** HuggingFace Transformers (`all-MiniLM-L6-v2`)
* **LLM Engine:** ChatGroq / Qwen / Google Gemini
* **Interface Layer:** Streamlit Studio Web UI Engine

## 🚀 Installation & Quick Start

Follow these sequential setup instructions to run the customer service assistant locally:

### 1. Project Ingestion
Clone your active version of the codebase repository:
```bash
git clone https://github.com/kamleshpatani/Agentic-AI.git
cd Agentic-AI/telecom_chatbot
```

### 2. Configure Token Parameters
Create your environment manager parameters template file:
```bash
cp .env.sample .env
```
Open your newly created `.env` file and append your API credentials securely (e.g., `GROQ_API_KEY=your_key_here`).

### 3. Setup Virtual Environment
Synchronize dependencies and container bounds:
```bash
uv sync
uv venv
source .venv/bin/activate
```

### 4. Index Knowledge Resources
Populate the localized Chroma database files by running the ingestion layer sequentially:
```bash
python ingest_faq.py
python ingest_tickets.py
python ingest_pdf.py
```
*Note: Successful execution will generate a localized `chroma_store/` target containing 25 FAQ vectors, 19 ticket vectors, and 37 PDF chunk vectors.*

### 5. Launch the Studio Dashboard
Initialize the visual runtime browser client:
```bash
streamlit run app.py
```