# 🧠 Tech ReportGen Pro

> **An AI-powered multi-agent technical report generator** built with Google Gemini, LangChain, LangGraph, and Gradio. Generate structured, fact-checked, 1000-word technical reports on **any technology topic** — with live web research and automatic reference generation.

---

## ✨ Features

- **🤖 Multi-Agent Pipeline** — Five specialized AI agents collaborate to produce a high-quality report:
  - **Subject Master** — Refines your topic into a focused report title
  - **Outliner** — Builds a structured 5-section outline
  - **Author** — Writes a detailed ~1000-word report in essay format
  - **Reviewer** — Fact-checks the draft using live web search and requests revisions if needed
  - **Citation Generator** — Automatically generates APA-formatted references

- **🌐 Live Web Research** — The Reviewer and Citation agents search the web in real-time:
  - Tries **Google Custom Search** first (if configured)
  - Automatically falls back to **DuckDuckGo** if Google Search is unavailable

- **📄 Download Reports** — Export generated reports as plain `.txt` files
- **📚 Auto References** — Generate a full references section with one click
- **🔄 Revise Draft** — Submit comments to refine and improve the generated report
- **🛡️ Quota Guard** — Gracefully handles Gemini API free-tier rate limits with friendly UI messages

---

## 🏗️ Architecture

```
User Prompt
    │
    ▼
Subject Master Agent  ──►  Refines topic
    │
    ▼
Outliner Agent        ──►  Creates structured outline
    │
    ▼
Author Agent          ──►  Writes ~1000-word draft
    │
    ▼
Reviewer Agent        ──►  Fact-checks via live web search
    │   ├─ Google Custom Search (primary)
    │   └─ DuckDuckGo (automatic fallback)
    │
    ▼
Final Report  ──►  Download TXT / Generate References
```

---

## 🚀 Getting Started

### Prerequisites

- Python 3.10+
- A [Google AI Studio API Key](https://aistudio.google.com/) (free)
- *(Optional)* A [Google Cloud Custom Search API Key](https://console.cloud.google.com/apis/credentials) + [Custom Search Engine ID](https://programmablesearchengine.google.com/)

---

### 1. Clone the Repository

```bash
git clone https://github.com/your-username/tech-reportgen-pro.git
cd tech-reportgen-pro
```

### 2. Create a Virtual Environment

```bash
python -m venv .venv

# Activate — Windows
.\.venv\Scripts\Activate.ps1

# Activate — macOS/Linux
source .venv/bin/activate
```

### 3. Install Dependencies

```bash
pip install -r requirements.txt
```

### 4. Configure Environment Variables

Copy the example file and fill in your keys:

```bash
cp .env.example .env
```

Edit `.env`:

```env
# Required: Gemini LLM key from https://aistudio.google.com/
GOOGLE_API_KEY=AIzaSy...

# Optional: Google Cloud API key for Google Custom Search
# If not set, DuckDuckGo is used automatically as fallback
GOOGLE_SEARCH_API_KEY=AIzaSy...

# Optional: Google Custom Search Engine ID
# Get it from https://programmablesearchengine.google.com/
GOOGLE_CSE_ID=your_cse_id_here
```

> **Note:** You only need `GOOGLE_API_KEY` to get started. Live web search falls back to DuckDuckGo automatically if Google Custom Search is not configured.

---

### 5. Run the App

```bash
python -m report_agent_app.gradioapp
```

Open your browser at: **http://127.0.0.1:7860**

---

## 🖥️ Usage

1. **Enter a topic** in the prompt box
   > e.g. *"Report about quantum computing"* or *"AI in healthcare"*

2. Click **Generate** — the agents will:
   - Analyze and refine the topic
   - Create an outline
   - Write a full technical report
   - Review and fact-check it with live search

3. **Download TXT** — save your report as a plain text file

4. **Generate References** — automatically produce APA-style citations

5. **Revise Draft** — type revision comments and click Generate again to refine the report

---

## 🔑 API Keys Guide

| Key | Required | Purpose | Where to Get |
|-----|----------|---------|-------------|
| `GOOGLE_API_KEY` | ✅ Yes | Gemini LLM for all AI agents | [Google AI Studio](https://aistudio.google.com/) |
| `GOOGLE_SEARCH_API_KEY` | ❌ Optional | Google Custom Search for fact-checking | [Google Cloud Credentials](https://console.cloud.google.com/apis/credentials) |
| `GOOGLE_CSE_ID` | ❌ Optional | Google Custom Search Engine ID | [Programmable Search Engine](https://programmablesearchengine.google.com/) |

> **`GOOGLE_API_KEY` and `GOOGLE_SEARCH_API_KEY` can be the same key** if it is a standard GCP API key (`AIzaSy...`).
> If you use a Google AI Studio key, provide a separate GCP key for `GOOGLE_SEARCH_API_KEY`.

---

## 📁 Project Structure

```
tech-reportgen-pro/
├── report_agent_app/
│   ├── __init__.py
│   ├── agent.py          # All AI agents, tools, and pipeline logic
│   ├── gradioapp.py      # Gradio UI and event handlers
│   ├── utils.py          # Prompt templates and helper functions
│   └── app.css           # Custom UI styling
├── .env                  # Your API keys (not committed to git)
├── .env.example          # Template for environment variables
├── requirements.txt      # Python dependencies
└── README.md
```

---

## ⚠️ Free Tier Limits

The app uses **Google Gemini 2.5 Flash** on the free tier, which has these limits:

| Limit | Value |
|-------|-------|
| Requests per minute | 5 RPM |
| Requests per day | 20–50 RPD |

**Each report generation uses ~4–5 requests.** If you hit a limit, the app displays a friendly warning instead of crashing. To remove limits, [enable billing](https://console.cloud.google.com/billing) on your Google Cloud project — generous free thresholds still apply.

---

## 🛠️ Tech Stack

| Component | Technology |
|-----------|-----------|
| LLM | Google Gemini 2.5 Flash |
| Agent Framework | LangGraph + LangChain |
| Search (Primary) | Google Custom Search API |
| Search (Fallback) | DuckDuckGo |
| UI | Gradio 6 |
| Fraud Detection | scikit-learn + joblib |

---

## 👨‍💻 Authors
- **Vicent** – [vicentmwanda](https://github.com/vicentmwanda)  
- **Fandresena** – [Efandresena](https://github.com/Efandresena)  

---

## 📄 License


MIT License — see [LICENSE](LICENSE) for details.

---

## 🙌 Acknowledgements

Built with ❤️ using:
- [Google Gemini API](https://ai.google.dev/)
- [LangChain](https://langchain.com/)
- [LangGraph](https://langchain-ai.github.io/langgraph/)
- [Gradio](https://gradio.app/)
- [DuckDuckGo Search](https://pypi.org/project/duckduckgo-search/)
