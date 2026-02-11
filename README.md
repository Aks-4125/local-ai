# InfinityAi — Presentation Notes

---

## 1. What is InfinityAi?

A **privacy-first, fully offline AI coding assistant** that runs entirely on your machine.

- Point it at your codebase → it indexes everything locally → ask questions about your code
- Powered by open-source LLMs running via **Ollama** — no cloud, no API keys, no data leaves your machine
- Built with Kotlin Multiplatform — runs on **Windows, macOS, and Android**

---

## 2. End User Requirements

| Requirement | Details |
|---|---|
| **OS** | Windows 10+ or macOS 12+ |
| **RAM** | 8 GB minimum (16 GB recommended for 14B models) |
| **Disk Space** | 10 GB free (for model downloads) |
| **Ollama** | Must be installed — [ollama.com](https://ollama.com) |
| **Internet** | Only needed once (to download models). After that, fully offline. |

### Setup (3 steps)
1. Install [Ollama](https://ollama.com) → run `ollama serve`
2. Download & launch InfinityAi
3. The wizard handles the rest (model download → project indexing → chat)

---

## 3. Privacy & Security — 100% Offline

> **No data ever leaves the user's machine.**

| Aspect | How It Works |
|---|---|
| **AI Engine** | Ollama runs locally — no cloud API calls |
| **Code Indexing** | Vector embeddings stored in a local JSON file inside the project |
| **Knowledge Graph** | Generated locally, saved to `.ai/knowledge_graph.json` |
| **Chat History** | Saved locally per-project |
| **Network** | Zero outbound network requests during operation |

**This means:**
- ✅ Safe for proprietary/enterprise codebases
- ✅ No data retention by third parties
- ✅ No API keys or accounts needed
- ✅ Works in air-gapped environments (after initial model download)

---

## 4. Models Used

| Model | Purpose | License | Commercial Use? | Link |
|---|---|---|---|---|
| **Qwen2.5-Coder 7B** | Chat (Default) | Apache 2.0 | ✅ Yes | [License](https://huggingface.co/Qwen/Qwen2.5-Coder-7B-Instruct/blob/main/LICENSE) |
| **Qwen2.5-Coder 14B** | Chat (Large) | Apache 2.0 | ✅ Yes | [License](https://huggingface.co/Qwen/Qwen2.5-Coder-14B-Instruct/blob/main/LICENSE) |
| **DeepSeek-R1 7B** | Chat (Reasoning) | MIT | ✅ Yes | [License](https://github.com/deepseek-ai/DeepSeek-R1/blob/main/LICENSE) |
| **DeepSeek-R1 14B** | Chat (Reasoning) | MIT | ✅ Yes | [License](https://github.com/deepseek-ai/DeepSeek-R1/blob/main/LICENSE) |
| **Qwen3-Embedding 0.6B** | Embeddings | Apache 2.0 | ✅ Yes | [License](https://huggingface.co/Qwen/Qwen3-Embedding-0.6B/blob/main/LICENSE) |

### ⚠️ Attribution Requirements

| Model | Requirement |
|---|---|
| **Qwen models** (Apache 2.0) | Must display **"Built with Qwen"** in product documentation if distributing a product that uses Qwen. If product exceeds 100M MAU, must request license from Alibaba Cloud. |
| **DeepSeek-R1** (MIT) | Include copyright notice and MIT license text. No other restrictions. |

---

## 5. Tools & Libraries — License Audit

| Tool / Library | License | Commercial Use? | Attribution Required? | Link |
|---|---|---|---|---|
| **Ollama** | MIT | ✅ Yes | Copyright notice only | [License](https://github.com/ollama/ollama/blob/main/LICENSE) |
| **Kotlin** | Apache 2.0 | ✅ Yes | License + copyright notice | [License](https://github.com/JetBrains/kotlin/blob/master/license/LICENSE.txt) |
| **Compose Multiplatform** | Apache 2.0 | ✅ Yes | License + copyright notice | [License](https://github.com/JetBrains/compose-multiplatform/blob/master/LICENSE.txt) |
| **Ktor Client** | Apache 2.0 | ✅ Yes | License + copyright notice | [License](https://github.com/ktorio/ktor/blob/main/LICENSE) |
| **Kotlinx Serialization** | Apache 2.0 | ✅ Yes | License + copyright notice | [License](https://github.com/Kotlin/kotlinx.serialization/blob/master/LICENSE.txt) |
| **Kotlinx Coroutines** | Apache 2.0 | ✅ Yes | License + copyright notice | [License](https://github.com/Kotlin/kotlinx.coroutines/blob/master/LICENSE.txt) |
| **Compottie** (Lottie) | MIT | ✅ Yes | Copyright notice only | [License](https://github.com/nicktaranov/compottie/blob/main/LICENSE) |

---

## 6. Commercial Use Summary

> **Can we use this commercially without declaring anything?**

**Short answer: Almost — but you need minor attributions.**

| What's Needed | Details |
|---|---|
| ✅ **No fees or royalties** | All models and tools are free for commercial use |
| ✅ **No special license requests** | Unless you exceed 100M MAU with Qwen models |
| ⚠️ **"Built with Qwen" notice** | Required in product documentation if distributing commercially |
| ⚠️ **Apache 2.0 / MIT license files** | Must be bundled with the distributed app (standard practice) |
| ✅ **No source code disclosure** | None of the licenses require you to open-source your code |

### Recommended Action Performed
Added a `THIRD_PARTY_LICENSES.md` file in the app bundle containing:
1. Apache 2.0 license text (covers Kotlin, Ktor, Compose, Qwen models)
2. MIT license text (covers Ollama, DeepSeek-R1)
3. A line: "Built with Qwen" (satisfies Qwen attribution)

**Now fully compliant for commercial distribution.**

---

## 7. Key Differentiators

| Feature | InfinityAi | Cloud AI Assistants |
|---|---|---|
| **Privacy** | 100% offline, zero data leakage | Code sent to cloud servers |
| **Cost** | Free (open-source models) | Per-token pricing |
| **Internet** | Not needed after setup | Always required |
| **Enterprise Ready** | Air-gapped compatible | Requires internet access |
| **Customization** | Choose your own model (easy to upgrade model in future) | Locked to provider's model |

---

## 8. Key Features

### 🔍 RAG-Powered Code Understanding
- Indexes your entire codebase into a **local vector database** using embeddings
- AI answers are **context-aware** — grounded in your actual code, not just general knowledge
- Retrieval-Augmented Generation ensures accurate, project-specific responses

### 🧠 Hive Mind (Knowledge Graph)
- Auto-generates an **architectural map** of your project (classes, functions, dependencies)
- Injected into every prompt so the AI deeply understands your project structure
- Stored locally at `.ai/knowledge_graph.json`

### ⚡ Smart / Differential Indexing
- Re-opening a project **only re-indexes new or modified files**
- Deleted files are automatically cleaned from the index
- Saves time on large codebases — no full re-indexing needed

### 👁️ Incremental File Watching
- **Real-time file system monitoring** detects file changes as you code
- Triggers instant re-indexing so the AI always has up-to-date context

### 💬 Streaming Responses
- Real-time **token-by-token** response streaming with live UI updates
- No waiting for the full response — see the answer as it's generated

### 🤔 Reasoning Model Support (DeepSeek-R1)
- Collapsible **"Thinking" UI** for DeepSeek-R1 chain-of-thought reasoning
- Parses `<think>` tags to show the AI's thought process before the final answer

### 📝 Rich Markdown Rendering
- Syntax-highlighted **code blocks** with copy-to-clipboard
- Collapsible sections, inline formatting (bold, italic, code), and bullet points

### 🔄 Multi-Model Selection
- Choose from **4 models**: Qwen2.5-Coder (7B/14B) or DeepSeek-R1 (7B/14B)
- License transparency — each model's license is shown during selection
- Configurable **context window** (default 32k tokens)

### 💾 Chat Persistence
- All chats are **saved per-project** and restored when you re-open
- Never lose your conversation history

### 🔥 Model Warm-Up
- Pre-loads the selected model into **GPU/RAM** on startup
- Ensures the first response is fast, with no cold-start delay

### 🎨 Premium Glassmorphism UI
- Glass-effect cards, **liquid animated backgrounds**, and dark mode
- Modern, polished design system built with Compose Multiplatform

### 📂 File Explorer & Single File Mode
- Built-in **tree view** with fuzzy search (exact, prefix, word-boundary, subsequence matching)
- **Single File Mode** — focus the AI on one file for quick code review

### 📑 Multi-Tab Chat
- Open **multiple chat sessions** and file viewers in tabs
- Work on different parts of your codebase simultaneously

### 🛑 Stop Generation
- **Cancel** in-progress AI responses at any time

### 🖥️ Cross-Platform
- Runs on **Windows** and **macOS** via Kotlin Multiplatform + Compose
