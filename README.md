# AI-Engineering-Core-Track

Collection of follow repos from beginner to intermediate AI engineering learning. This will follow several comprehensive courses out there to teach fundamental concepts and practice questions to reinforce the concepts on practical usecases.

# REPO 1: Udemy-EdDonner-MasterAIAndLLMs

Personal follow-along repo for Ed Donner's **"LLM Engineering: Master AI, Large Language Models & Agents"** Udemy course.

This is not a tutorial/reference repo — it's a working log of the course. Each week is a folder; each day in that week has:
- a **lesson notebook** (`dayN.ipynb`, or a descriptively-named equivalent in week1) — followed along with the course video, and
- a **practice notebook** (`dayN-<ProjectName>.ipynb`) — my own build applying that day's concepts, done to cement the material.

Weeks also end with an official `weekN EXERCISE.ipynb` assignment from the course.

Currently covers **Week 1** and **Week 2**. (`.gitignore` already has entries reserved for weeks 4–8, so more will land as the course progresses.)

## Setup

Everything lives under `Udemy-EdDonner-MasterAIAndLLMs/`, managed with [uv](https://docs.astral.sh/uv/):

- `pyproject.toml` / `uv.lock` — dependencies: `openai`, `anthropic`, `google-genai`, `groq`, `ollama`, `litellm`, `langchain` (+ `-openai`/`-anthropic`/`-ollama`/`-chroma`/`-huggingface` variants), `gradio`, `chromadb`, `transformers`, `datasets`, `sentence-transformers`, `torch`, `scikit-learn`, `xgboost`, `pandas`, `plotly`, `wandb`, and friends.
- `.python-version` — pinned to `3.12.12`.
- `.env` (gitignored) — provider API keys (OpenAI, Anthropic, Google/Gemini, DeepSeek, Groq, Grok, OpenRouter). Loaded via `python-dotenv`.
- `util.py` — shared helper used across notebooks: `check_api_key("openai")` prints whether a provider's key is set (and previews the first few chars); `load_keys()` checks every known provider at once.

Run notebooks with `uv run jupyter lab` (or open in VS Code/Cursor with the `uv`-managed `.venv` as the kernel) from inside `Udemy-EdDonner-MasterAIAndLLMs/`.

Some notebooks default to paid frontier APIs (OpenAI/Anthropic/Gemini) but have an [Ollama](https://ollama.com/) (free, local) alternative noted inline.

## Week 1 — Frontier APIs & your first LLM projects

| Notebook | Type | What it does |
|---|---|---|
| `BuildingWebsiteSummarizerUsingOpenAIAPI.ipynb` | Lesson (Day 1) | First Frontier LLM project — calls the OpenAI Chat Completions API to summarize a scraped website. |
| `RunningOllamaLocally.ipynb` | Lesson (Day 2) | Upgrades the Day 1 project to run against a local open-source model via Ollama instead of OpenAI. |
| `WebsiteSummarizerUsingOllama.ipynb` | Practice (Day 2) | Own build of the Ollama-based summarizer, using `scraper.py` + `solution.py`. |
| `ContextWindowAndTokenLimit.ipynb` | Lesson (Day 4) | Tokenizing text with `tiktoken`, context window limits, and why LLMs don't have real "memory" between calls. |
| `BrochureGeneratorWithGPT4.ipynb` | Practice | Extends the Day 1 project: scrapes a company site, has the model pick relevant links (one-shot JSON prompting), then assembles a streamed markdown company brochure. |
| `DSABuddy.ipynb` | Practice (self-directed) | A tutor that explains any data-structures/algorithms concept on request. |
| `week1 EXERCISE.ipynb` | Assignment | Official end-of-week brief: build a tool that takes a technical question and explains it, using both OpenAI and Ollama. |
| `Week1Exercise-TechnicalTutor.ipynb` | Practice (assignment attempt) | My attempt at the Week 1 exercise — currently a stub/WIP. |
| `scraper.py` | Helper | `fetch_website_contents(url)` / `fetch_website_links(url)` — BeautifulSoup-based scraping used by several notebooks. |
| `solution.py` | Helper | Ollama-backed website summarizer (snarky-summary system prompt), used by `WebsiteSummarizerUsingOllama.ipynb`. |

## Week 2 — Frontier model APIs, UIs, and tool calling

| Notebook | Type | What it does |
|---|---|---|
| `day1.ipynb` | Lesson | Connects to OpenAI, Anthropic and Gemini APIs directly; training vs. inference-time scaling. |
| `day1-ThreeWayChat.ipynb` | Practice | A 3-way conversation loop between GPT, Claude and Gemini (via `litellm`), each responding to the other two. |
| `day2.ipynb` | Lesson | Building UIs with Gradio: basic interface, share links, adding auth. |
| `day2-CompanyBrochure.ipynb` | Practice | Own version of the company-brochure generator, using `util.check_api_key` for key handling. |
| `day3.ipynb` | Lesson | Conversational AI — building a chatbot with a `chat(message, history)` Gradio callback, system prompts, one-shot examples. |
| `day3-Chatbot.ipynb` | Practice | A Gradio chatbot that gives kids healthy snack suggestions. |
| `day4.ipynb` | Lesson/Project | Airline AI Assistant — introduces tool/function calling so the LLM can invoke local functions, including multiple tool calls per response. |
| `day5.ipynb` | Lesson/Project | Extends the Airline AI Assistant: multi-modal — DALL-E-3 image generation (`artist()`), audio, tool calling with a "database" lookup — a step toward an agentic workflow. |
| `extra.ipynb` | Bonus | Gets frontier models (via OpenRouter) to generate an SVG of a pelican riding a bike, inspired by Simon Willison's benchmark. |
| `week2 EXERCISE.ipynb` | Assignment | Official end-of-week brief: turn the Week 1 technical-Q&A tool into a full Gradio prototype with streaming, model switching, and (bonus) tool use. |
| `scraper.py` | Helper | Same scraping helper as week1's copy. |
| `revealer.py` | Helper | `reveal(svg)` — animates an SVG's shapes into view one-by-one (CSS keyframe reveal), used in `extra.ipynb`. |
| `hamlet.txt` | Data | Sample text asset used in one of the notebooks. |
