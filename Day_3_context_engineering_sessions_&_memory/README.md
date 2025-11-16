---

# Kaggle 5‑Day Agents Course — Day 3: Memory & Sessions  

This repository contains the notebooks for **Day 3** of the Kaggle 5‑Day Agents Course, focusing on **memory management** using the **Google Agent Development Kit (ADK)**.  

In this module, you’ll learn how to build **stateful agents** that can remember information both within a single conversation (short‑term memory) and across multiple conversations (long‑term memory).  

---

## 📂 Notebooks Included  

### `day-3a-agent-sessions.ipynb` — *Part 1: Session Management*  
**Concept**: Manage short‑term memory within a single conversation thread.  
**Key Topics**:  
- Understanding **Sessions, Events, and State**  
- Using `InMemorySessionService` for temporary state  
- Using `DatabaseSessionService` (SQLite) for persistent sessions that survive restarts  
- Managing long conversations efficiently with **Context Compaction**  
- Creating custom tools to read/write from `session.state`  

---

### `day-3b-agent-memory.ipynb` — *Part 2: Memory Management*  
**Concept**: Build a long‑term, searchable knowledge store for your agent.  
**Key Topics**:  
- Difference between **short‑term Sessions** and **long‑term Memory**  
- Populating memory with `add_session_to_memory()`  
- Retrieving information via `load_memory` (reactive) and `preload_memory` (proactive) tools  
- Automating memory storage using ADK callbacks (`after_agent_callback`)  
- Conceptual overview of **Memory Consolidation** (extracting key facts from raw conversation)  

---

## 🚀 Getting Started  

### 1. Prerequisites  
- Python 3  
- Install Google ADK:  
```bash
pip install google-adk
```  

### 2. Configure Your Gemini API Key  
These notebooks require a Gemini API key.  

- **Get your API key**: Create one in *Google AI Studio*.  
- **Add to Kaggle Secrets**:  
  - In Kaggle notebook editor → *Add‑ons > Secrets*  
  - Create a new secret labeled `GOOGLE_API_KEY`  
  - Paste your key into the **Value** field → Save  
  - Ensure the checkbox next to `GOOGLE_API_KEY` is selected to attach the secret  

### 3. Running the Notebooks  
- Open either `.ipynb` file in Jupyter (Kaggle, Colab, or VS Code).  
- Run cells **top to bottom**.  
- ⚠️ Important: Avoid using **“Run All”** — this may trigger rate limits (429 errors) with Gemini API.  

---

## ℹ️ Course Information  

- These notebooks are for **hands‑on practice and learning**.  
- No submission is required to complete the course.  
- For help, join the **Kaggle Discord server** mentioned in the notebook instructions.  

---

✨ *Day 3 builds the foundation for agents that can “remember” — enabling richer, more contextual interactions across sessions and conversations.*  

---