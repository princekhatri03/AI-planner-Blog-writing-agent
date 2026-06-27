# 📘 LangGraph AI Blog Generator

An end-to-end AI-powered technical blog generation system built using LangGraph, LLMs, and structured outputs.  
The system automatically plans, researches, and writes high-quality technical blog posts using a multi-agent workflow.

---

## 🚀 Features

- 🧠 LLM-powered blog planning (Orchestrator agent)
- 🔍 Web research integration using Tavily API
- 🧩 Structured outputs using Pydantic schemas
- ⚙️ LangGraph multi-agent workflow
- ✍️ Section-wise blog generation
- 🖼️ Image prompt + placeholder generation
- 🔁 Parallel worker execution (fan-out architecture)
- 📦 Strict JSON output handling for reliability

---

## 🏗️ Architecture
```text
User Input
↓
Router (decides mode: closed / hybrid / open)
↓
Research Node (Tavily API)
↓
Orchestrator (creates blog plan)
↓
Fan-out Workers (generate sections)
↓
Image Generator (optional)
↓
Final Markdown Blog
```
---

## 🧠 Workflow Breakdown

### 1. Router Node
- Decides whether research is required
- Outputs:
  - mode (`closed_book`, `hybrid`, `open_book`)
  - queries (if needed)

---

### 2. Research Node
- Uses Tavily Search API
- Collects relevant sources
- Converts results into structured evidence

---

### 3. Orchestrator Node
- Generates blog outline
- Splits into sections (tasks)
- Each task includes:
  - goal
  - bullets
  - tags
  - word count
  - code requirements

---

### 4. Worker Node
- Writes one section at a time
- Uses evidence when available
- Outputs Markdown content

---

### 5. Image Generator Node
- Creates image prompts
- Inserts placeholders into Markdown
- Optionally integrates image APIs

---

## 🛠️ Tech Stack

- Python 3.10+
- LangGraph
- LangChain
- Pydantic
- Hugging Face / Gemini / OpenAI
- Tavily Search API
- Markdown

---

## 📦 Installation

```bash
git clone https://github.com/your-username/langgraph-blog-generator.git
cd langgraph-blog-generator

python -m venv venv

# Windows
venv\Scripts\activate

pip install -r requirements.txt
```

---

## 🔑 Environment Variables

Create a `.env` file in the root directory:

```env
GOOGLE_API_KEY=your_google_api_key
TAVILY_API_KEY=your_tavily_api_key

# Optional (if using Hugging Face)
HUGGINGFACEHUB_API_TOKEN=your_token
```

---

## ▶️ Run Project

```bash
python main.py
```

---

## 📁 Project Structure

```text
project/
│
├── graph/
│   ├── router.py
│   ├── orchestrator.py
│   ├── worker.py
│   ├── research.py
│
├── schemas/
│   ├── plan.py
│   ├── router.py
│   ├── evidence.py
│
├── tools/
│   ├── tavily.py
│   ├── image_gen.py
│
├── main.py
├── README.md
```
## ⚠️ Known Issues
```text
Hugging Face Inference API may hit:
402 (quota exhausted)
429 (rate limits)
JSON parsing errors if model output is not strictly structured
Parallel workers may exceed API limits
```
---
## 💡 Tips
```text
Use temperature = 0 for structured outputs
Reduce worker fan-out during testing
Add retry/backoff for API limits
Cache intermediate results
Prefer Gemini/OpenAI structured output for stability
```
---
## 🧠 Future Improvements
```text
Streamlit UI
Streaming blog generation
Vector DB memory
Multi-model routing (cheap vs premium)
Auto publish to Medium / Dev.to
```
