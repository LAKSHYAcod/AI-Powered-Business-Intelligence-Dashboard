# 🤖 AI-Powered BI Dashboard (LangChain + LangGraph)

A simplified but **technically complete** BI dashboard using:
- **LangChain** for LLM text-to-SQL generation
- **LangGraph** for query workflow orchestration (generate → validate → execute)
- **Streamlit** for the UI
- **SQLite** for data storage (zero config)

## 🚀 Quick Start

### 1. Extract & Install
```bash
cd ai_bi_dashboard_simple
python -m venv venv

# Windows
venv\Scripts\activate

# macOS/Linux
source venv/bin/activate

pip install -r requirements.txt
```

### 2. Seed Database
```bash
python seed_data.py
```
Creates:
- Users: `admin`/`admin123`, `analyst`/`analyst123`
- Tables: `sales` (500 rows), `finance` (12 rows), `inventory` (100 rows)

### 3. Run
```bash
streamlit run app.py
```
Open **http://localhost:8501**

## 🔑 Optional: Enable AI Queries

Get a free key from [openrouter.ai](https://openrouter.ai), then:
```bash
echo "OPENROUTER_API_KEY=sk-or-v1-your-key" > .env
```

Without this key, all features work except the AI text-to-SQL (shows config message).

## 🏗️ Architecture

```
User Question
    ↓
LangChain (ChatOpenAI + PromptTemplate) → generates SQL
    ↓
LangGraph StateGraph:
  Node 1: generate_sql()
  Node 2: validate_sql()  ← checks for forbidden operations
  Node 3: execute_sql()   ← runs if validation passed
    ↓
Results + Auto Chart
```

## 📁 Files

| File | Purpose |
|------|---------|
| `app.py` | Streamlit UI |
| `services.py` | **LangChain + LangGraph** logic, insights, alerts, charts |
| `database.py` | SQLite setup |
| `seed_data.py` | Sample data generator |
| `requirements.txt` | Dependencies (includes langchain, langgraph) |

## 📝 Tech Stack

- `langchain` + `langchain-openai` — LLM integration
- `langgraph` — Workflow orchestration (StateGraph)
- `streamlit` — Frontend
- `sqlite3` — Database (built into Python)
- `plotly` — Charts
- `scikit-learn` + `statsmodels` — Predictive analytics
