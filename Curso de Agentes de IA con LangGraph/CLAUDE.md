# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Educational Jupyter notebook for an AI Agents course using LangChain, LangGraph, and Google's Gemini 2.5 Flash model via Vertex AI. All course content lives in a single notebook: `Curso de Agentes de IA con LangGraph.ipynb`.

## Setup

**Install dependencies:**
```bash
pip install -q -U langchain langchain-community langgraph langchain-google-genai \
    langchain-tavily google-auth python-dotenv arxiv tavily-python
```

**Authenticate with Google Cloud (run once):**
```bash
gcloud auth login
gcloud auth application-default login
gcloud config set project YOUR_PROJECT_ID
```

**Environment variables** — create `.env` in the project root:
```
GOOGLE_CLOUD_PROJECT=your-project-id
TAVILY_API_KEY=your-tavily-api-key
```

**Run the notebook:**
```bash
jupyter notebook "Curso de Agentes de IA con LangGraph.ipynb"
```

## Architecture

The notebook follows a linear 5-step structure:

1. **Dependency installation** — pip installs inside the notebook
2. **Google Cloud ADC authentication** — explained as a one-time terminal step
3. **Environment setup** — loads `.env` via `python-dotenv`, imports LangChain/LangGraph
4. **Model + tools initialization** — the core agent setup
5. **Tool invocation test** — manual testing of the agent's tools

### Core agent pattern

Authentication uses ADC (`google.auth.default()`) rather than an API key — credentials are passed explicitly to `ChatGoogleGenerativeAI`:

```python
credentials, project_id = google.auth.default()
llm = ChatGoogleGenerativeAI(model="gemini-2.5-flash", credentials=credentials)
```

Tools are defined with the `@tool` decorator and bound to the model via `llm.bind_tools(tools)`, producing `llm_con_herramientas`. The two tools in the notebook are:
- `busca_web(query)` — wraps `TavilySearch(max_results=5)`
- `multiplicar(a, b)` — returns `a * b`

Tool calls are extracted from `response.tool_calls[0]["args"]` and invoked manually, simulating what a LangGraph agent does autonomously.
