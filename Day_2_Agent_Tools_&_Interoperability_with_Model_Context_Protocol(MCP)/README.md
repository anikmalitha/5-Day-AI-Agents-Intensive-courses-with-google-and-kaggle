# Day 2 — Agent Tools & Interoperability with Model Context Protocol (MCP)  

Welcome to **Day 2** of the *5‑Day Agentic AI Course*!  
This session moves beyond basic agents into building powerful, actionable agents that can interact with the world, execute code, and perform complex, multi‑step tasks.  

---

## 📌 Overview  

Day 2 is split into two main parts:  
1. **Agent Tools** — Creating custom tools from Python functions and using other agents as tools.  
2. **Tool Patterns & Best Practices** — Connecting to external services via MCP and building resumable workflows with human approval (Long‑Running Operations).  

---

## 🧠 What We Learned  

### Part 1: Building Custom Agent Tools (`day-2a-agent-tools.ipynb`)  

- **Why Tools Matter**: Tools give agents access to live data, overcome knowledge cutoffs, and enable real‑world actions.  

#### 🛠️ Key Learning 1: Custom Function Tools  
- Any Python function can be turned into a tool.  
- Example: A **Currency Converter agent** using `get_fee_for_payment_method` and `get_exchange_rate`.  
- **Best Practices**:  
  - Clear docstrings → help the LLM understand usage.  
  - Type hints → ensure correct schema generation.  
  - Structured returns → use dictionaries (`{"status": "success"}` / `{"status": "error"}`) for clarity.  

#### 🤖 Key Learning 2: Agents as Tools (Reliable Code Execution)  
- LLMs are unreliable at complex math.  
- Solution: Delegate tasks to specialist agents.  
- Example:  
  - `calculation_agent` executes Python code via `BuiltInCodeExecutor()`.  
  - Wrapped with `AgentTool(agent=calculation_agent)` and used by `enhanced_currency_agent`.  
- Pattern: A “manager” agent delegates specialized tasks to “specialist” agents.  

---

### Part 2: Advanced Tool Patterns (`day-2b-agent-tools-best-practices.ipynb`)  

#### 🌐 Key Learning 3: Model Context Protocol (MCP)  
- **What**: An open standard for agent interoperability with external services (GitHub, Slack, Maps, DBs).  
- **How**: Use `McpToolset` to connect agents to MCP servers.  
- **Example**: Connected to `@modelcontextprotocol/server-everything` and used its `getTinyImage` tool seamlessly.  

#### ⏳ Key Learning 4: Long‑Running Operations (Human‑in‑the‑Loop)  
- Agents can pause, request human approval, and resume.  
- **Use Cases**: Financial transactions, bulk deletions, high‑cost operations.  
- **Example**: `place_shipping_order` tool:  
  - Auto‑approves small orders (≤5 containers).  
  - Pauses for human approval on large orders (>5 containers).  

**Workflow Components**:  
1. **Tool (`place_shipping_order`)**  
   - Accepts `tool_context: ToolContext`.  
   - Calls `tool_context.request_confirmation(...)` → returns `{"status": "pending"}`.  
   - Resumes with human decision via `tool_context.tool_confirmation`.  

2. **App (`ResumabilityConfig`)**  
   - Wrap agent in `App` with `is_resumable=True`.  
   - Enables state saving and resumability.  

3. **Workflow (Calling Code)**  
   - Run agent with `shipping_runner.run_async(...)`.  
   - Capture `invocation_id`.  
   - Detect `adk_request_confirmation` event → pause.  
   - Resume with human decision + original `invocation_id`.  

---

## 📊 Summary: Day 2 Key Concepts & Components  

| Component              | What It Is                                   | When to Use It                                      |
|------------------------|-----------------------------------------------|-----------------------------------------------------|
| **FunctionTool**       | Custom Python function as a tool              | For business logic (e.g., `get_exchange_rate`)      |
| **BuiltInCodeExecutor**| Built‑in sandboxed Python executor            | For reliable math or data processing                |
| **AgentTool**          | Wraps one agent as a tool for another         | To delegate specialized tasks                       |
| **McpToolset**         | Connects agents to external MCP servers       | To use 3rd‑party services without custom API clients|
| **ToolContext**        | Auto‑passed argument to tools                 | For long‑running tools that can pause               |
| **request_confirmation()** | Pauses agent execution for approval       | For human‑in‑the‑loop workflows                     |
| **App & ResumabilityConfig** | Enables state saving/resumability       | Required for pausable operations                    |
| **invocation_id**      | Unique ID for agent execution run             | To resume paused sessions                           |  

---

## 🚀 Quick Start  

1. Open notebooks:  
   - VS Code → *File → Open Folder* → select repo root → open notebooks.  
   - Jupyter → run `jupyter notebook` or `jupyter lab`.  
2. Run cells in:  
   - `day-2a-agent-tools.ipynb`  
   - `day-2b-agent-tools-best-practices.ipynb`  
3. Experiment with custom tools, MCP integrations, and long‑running workflows.  

---

## ⏭ Next Steps  

Proceed to **Day 3** to explore **multi‑agent collaboration, environment integration, and advanced orchestration patterns**.  

---

✨ *This repository documents my journey through the 5‑Day Agentic AI Course. Each day builds on the last, moving from fundamentals to advanced agent interoperability and orchestration.*  
