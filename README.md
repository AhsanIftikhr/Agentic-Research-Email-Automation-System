# Agentic Research & Email Automation System

AI-powered research automation workflow built with n8n integrating Claude Sonnet 4.6, Tavily Search API, Redis memory store, SMTP email delivery, AI decision-making, deduplication, and structured execution logging.

---

## 🚀 Features

- Automated AI-powered research using Tavily API
- LLM-based parsing & decision making using Claude Sonnet 4.6
- Automated HTML email generation & delivery
- Redis-based memory & duplicate prevention
- AI routing decisions:
  - send
  - ignore
  - escalate
- Error handling & retry/fallback logic
- Structured execution logging
- Secure environment variable credential management
- Fully modular workflow architecture

---

## 🏗 Workflow Architecture

```text
Webhook Trigger
      ↓
Input Processing
      ↓
Research Layer (Tavily API)
      ↓
Parsing via Claude
      ↓
Parsing & Filtering
      ↓
Memory Check (Redis)
      ↓
Deduplication Branch
   ┌───────────────┐
New Topic      Duplicate
   ↓               ↓
AI Decision    Skip Log
   ↓
Decision Branch
 ┌───────────────┐
Send         Ignore
 ↓               ↓
SMTP Email    Logging
 ↓
Redis Store
 ↓
Execution Logging
 ↓
Webhook Response
```

---

## 🧩 Tech Stack

| Component | Technology |
|---|---|
| Workflow Engine | n8n |
| LLM | Claude Sonnet 4.6 |
| Research API | Tavily Search API |
| Memory Store | Redis |
| Email Service | SMTP |
| Backend Logic | JavaScript (n8n Code Nodes) |
| Trigger | n8n Webhook |

---

## 📂 Repository Structure

```text
├── workflow.json
├── execution_logs.json
├── report.pdf
├── screenshots/
├── README.md
└── .env.example
```

---

## ⚙️ Environment Variables

Create a `.env` file:

```env
TAVILY_API_KEY=your_tavily_api_key
ANTHROPIC_API_KEY=your_anthropic_api_key

SMTP_HOST=smtp.example.com
SMTP_PORT=587
SMTP_USER=your_email
SMTP_PASS=your_password

REDIS_HOST=localhost
REDIS_PORT=6379
REDIS_PASSWORD=your_password
```

---

## 🔌 API Integrations

### Tavily Research API

Used for:
- External web research
- Fetching latest AI-related information
- Retrieving structured search results

### Claude Sonnet 4.6

Used for:
- Parsing search results
- Confidence scoring
- AI decision making
- HTML email generation
- Insight extraction

---

## 🧠 AI Decision Logic

The workflow intelligently decides:

| Decision | Action |
|---|---|
| send | Email report sent |
| ignore | No email sent |
| escalate | Email sent with escalation flag |

Decision is based on:
- Research confidence scores
- Topic priority
- Audience type
- Result quality

---

## 🛡 Advanced Features

### ✅ Deduplication System
Redis TTL prevents duplicate topic processing within 24 hours.

### ✅ Error Handling
Graceful fallback using:
- onError: continueErrorOutput
- Dedicated Error Logger node

### ✅ Validation Gates
Before sending emails:
1. Confidence filtering
2. Deduplication check
3. JSON validation

### ✅ Structured Logging
Every execution path is logged:
- Success
- Duplicate
- Ignore
- Escalation
- Error

---

## 📊 Sample Input Payload

```json
{
  "topic": "AI automation trends",
  "audience": "technical lead",
  "priority": "high"
}
```

---

## 📤 Sample AI Decision Output

```json
{
  "decision": "send",
  "reason": "High-priority topic with strong results.",
  "email_subject": "[Research Report] AI Automation Trends",
  "insights": [
    "Agentic AI pipelines replacing rule-based automation"
  ]
}
```

---

## ▶️ How To Run

### 1. Clone Repository

```bash
git clone https://github.com/yourusername/agentic-research-email-automation.git
cd agentic-research-email-automation
```

### 2. Start Redis

```bash
docker run -d -p 6379:6379 redis
```

### 3. Start n8n

```bash
docker run -it --rm \
-p 5678:5678 \
--env-file .env \
n8nio/n8n
```

### 4. Import Workflow

Import `workflow.json` into n8n.

### 5. Trigger Workflow

```bash
curl -X POST http://localhost:5678/webhook/research-trigger \
-H "Content-Type: application/json" \
-d '{
  "topic":"AI automation trends",
  "audience":"technical lead",
  "priority":"high"
}'
```

---

## 📈 Execution Scenarios

Implemented scenarios:
- Successful Send
- Duplicate Detection
- AI Ignore
- Escalation
- API Failure Handling
- Retry Logic

---

## 📸 Recommended Screenshots For Repo

Add screenshots of:
- Full workflow canvas
- Successful execution
- Redis memory
- SMTP email output
- Execution logs

Store inside:

```text
/screenshots
```

---

## 🎯 Assignment Requirements Covered

| Requirement | Status |
|---|---|
| External LLM API | ✅ |
| AI Decision Layer | ✅ |
| Email Integration | ✅ |
| External Research | ✅ |
| Memory/Deduplication | ✅ |
| Structured Logging | ✅ |
| Retry/Fallback Logic | ✅ |
| JSON Structured Output | ✅ |
| Branching Logic | ✅ |
| Validation Gates | ✅ |

---

## 👨‍💻 Author

Ahsan Iftikhar  
BS Artificial Intelligence  
FAST NUCES

---

