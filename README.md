
🛍️ AI Shopping Agent

An intelligent, autonomous AI Shopping Assistant built with Python, Streamlit, and SQLite. Inspired by Amazon's Rufus, this agent handles conversational product searches, processes multi-modal image inputs to find similar products, computes real-time product rating analytics, handles out-of-scope requests gracefully, and safely executes autonomous checkouts.

✨ Key Features

• Natural Language Product Discovery: Search inventory using flexible conversational inputs. The backend features tolerant substring containment lookups that gracefully handle spelling variations and typos (e.g., matching "organics" to "organic").
• Dynamic Review Aggregation: Automatically crawls and calculates real-time aggregate star ratings and review counts from relational schemas using mathematical modular routines.
• Autonomous Checkout System: Interprets user intent to interact directly with transactional state histories, securely placing orders and logging them inside the database.
• Multimodal Image Search: Upload a snapshot of any product (like oats) to extract structural aesthetics using Vision LLMs and query similar items.
• Out-of-Scope Exception Handling: Safe operational guardrails protect the engine from processing invalid catalog targets (e.g., trying to purchase an "elephant").


🏗️ System Architecture & Data Schema

The project relies on a structured, normalized local SQLite relational storage engine (store.db) composed of three main schemas:

ai-shopping-agent/
│
├── store.db                  # Local SQLite database
├── app.py                    # Streamlit app
├── setup_db.py               # setup SQLite database
├── reviews_api.py            # Core analytics engine for computing metrics
├── shopping_agent.py         # Streamlit UI & Multi-tool AI Agent orchestration
├── .env.example              # Public structural configuration template
└── README.md                 # Project documentation


Database Tables Breakdown

1. products: Stores catalog data containing columns like id, name, category, price, description, and is_organic.
2. reviews: Tracks user evaluation inputs containing review_id, product_id, username, rating, and comment. Used to compute dynamic star aggregates.
3. orders: An immutable transaction history ledger recording order_id, product_id, product_name, price, and ordered_at.


🛠️ Tech Stack

• Interface Layer: Streamlit Studio Web Engine
• Data Layout: SQLite Relational Database Engine
• LLM Orchestration: ChatGroq / Google Gemini Multimodal APIs
• Environment Management: Python dotenv


🚀 Quick Start & Installation

Follow these quick implementation blocks to run this agent locally on your machine.

1. Clone the Project Assets

bash
git clone https://github.com
cd YOUR-REPO-NAME


2. Set Up a Clean Virtual Environment

bash
# Initialize environment
python -m venv venv

# Activate on Windows:
venv\Scripts\activate
# Activate on macOS/Linux:
source venv/bin/activate

3. Install Dependencies & Setup Configurations

Ensure you have streamlit and standard library components ready. Create your secure configuration tracker file:
bash
cp .env.example .env

Open your newly created .env file and append your custom API credentials (e.g., GROQ_API_KEY=your_key_here or GEMINI_API_KEY=your_key_here).

4. Boot Up the Agent Studio Engine

bash
streamlit run app.py

