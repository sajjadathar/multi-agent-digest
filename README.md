# 🧠 multi-agent-digest

A modular, Dockerized multi-agent AI system that turns raw text inputs (newsletters, notes, articles) into a clean, prioritized daily Markdown digest.

Built with Python, Docker, and Docker Compose.

---

## 🚀 What This Project Does

This system runs four specialized agents in sequence:

1. **Ingestor** → Collects and combines raw text files  
2. **Summarizer** → Uses an LLM to extract key insights  
3. **Prioritizer** → Scores items by urgency keywords  
4. **Formatter** → Generates a clean Markdown daily digest  

Each agent runs in its own isolated Docker container.

---

## 🏗 Architecture

```
Input Files
↓
Ingestor
↓
Summarizer (LLM)
↓
Prioritizer
↓
Formatter
↓
daily_digest.md
```

- Shared `/data` volume for internal communication  
- `/output` volume for final digest  
- Sequential execution enforced by Docker Compose  

---

## 📂 Project Structure

```
multi-agent-digest/
├── agents/
│   ├── ingestor/
│   ├── summarizer/
│   ├── prioritizer/
│   └── formatter/
├── data/input/
├── output/
├── tests/
├── docker-compose.yml
├── .env
└── README.md
```

---

## ⚙️ Requirements

- Python 3.10+
- Docker (Engine 20.10+)
- Docker Compose v2
- OpenAI API Key (for summarizer)

---

## 🔐 Setup

### 1️⃣ Clone the Repository

```bash
git clone https://github.com/your-username/multi-agent-digest.git
cd multi-agent-digest
```

### 2️⃣ Add Your API Key

Create a `.env` file in the project root:

```
OPENAI_API_KEY=sk-your-key-here
```

⚠️ Never commit `.env` to GitHub.

### 3️⃣ Add Input Files

Place `.txt` files inside:

```
data/input/
```

---

## ▶️ Run the Pipeline

```bash
docker compose up --build
```

After completion, open:

```
output/daily_digest.md
```

---

## 🧪 Run Tests

```bash
pip install pytest
python -m pytest tests/ -v
```

---

## 🔄 Automate Daily Execution (Linux/macOS)

Add to crontab:

```bash
0 7 * * * cd /path/to/project && docker compose up --build >> cron.log 2>&1
```

---

## 🛡 Security Notes

- API keys stored in `.env`
- Containers use minimal `python:3.x-slim` base images
- LLM failures handled gracefully
- Retry logic included for rate limits

For production:
- Use Docker Secrets
- Add resource limits
- Consider Kubernetes Jobs for scaling

---

## 💡 Why Multi-Agent?

Instead of one large prompt ("God Model"), this system:

- Separates concerns
- Reduces hallucination risk
- Improves testability
- Allows independent scaling
- Minimizes LLM cost

Only the **Summarizer** calls an LLM.  
All other agents are deterministic Python.

---

## 🧠 Example Output

```markdown
# Your Daily AI Digest

**Date:** 2026-02-26

## Top Insights

- **Priority 2**: IMPORTANT: Deadline this Friday
- **Priority 1**: URGENT: Regulation update
- **Priority 0**: General AI news
```

---

## 🚀 Future Improvements

- Replace volume-based communication with Redis
- Add Slack or email delivery
- Add metrics + Prometheus monitoring
- Support local LLM via Ollama
- Convert to Kubernetes CronJob

---

## 📜 License

MIT License

---

## ✨ Author

Built as a practical example of containerized multi-agent AI workflows using Python and Docker.

---

If this project helped you, consider ⭐ starring the repo.