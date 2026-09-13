# Task #13: Agent Concepts and MCP Basics (FL-05)

**Track**: General AI Fluency  
**Phase**: Build (core)  
**Intern**: Ghulam Qasim (FlyRank Machine Learning & AI Fluency Intern)  
**Email**: qaximkhaskheli@gmail.com  
**Program URL**: [FlyRank AI Fluency - Week 04](https://aifluency.flyrank.ai/week-04.html#agent-concepts-and-mcp-basics)  

---

## 📌 Executive Summary

Understanding the distinction between deterministic workflows and dynamic agents—and how the Model Context Protocol (MCP) enables LLMs to interact with external tools—is essential for evaluating AI architecture. This assignment (FL-05) presents a 780-word technical explainer, evidence of active MCP tool calls, and an agent upgrade roadmap for the FL-04 pipeline.

---

## 🛠️ Evidence of Working MCP Tool Execution (3 Tasks Chat Alone Cannot Do)

Standard conversational AI chat cannot inspect local file systems, query directory trees, or parse real-time repository state. Using an active MCP server client, the following three tasks were executed using tool calls:

### Task 1: Autonomous Workspace Directory Inspection (`list_dir`)
- **Tool Executed**: `list_dir(DirectoryPath="q:\\FlyRank AI Intern\\AI Fluency Assignment Tasks")`
- **Output Capability**: Analyzed local workspace file system, discovering existing task folders (`#1` through `#12`), file sizes, and last-modified timestamps.
- **Why Chat Alone Cannot Do This**: Base LLM chat has no access to local disk hardware or operating system file handles.

---

### Task 2: Real-Time Local Source File Retrieval (`view_file`)
- **Tool Executed**: `view_file(AbsolutePath="q:\\FlyRank AI Intern\\AI Fluency Assignment Tasks\\#12 Ship an Automation Workflow\\README.md")`
- **Output Capability**: Read exact raw file contents and line ranges from local disk storage to verify workflow configuration details.
- **Why Chat Alone Cannot Do This**: Chat models only process static context provided in the initial prompt window; MCP allows dynamic file system retrieval on demand.

---

### Task 3: Multi-File Codebase Pattern Search (`grep_search`)
- **Tool Executed**: `grep_search(Query="FastAPI", SearchPath="q:\\FlyRank AI Intern\\AI Fluency Assignment Tasks")`
- **Output Capability**: Scanned across all workspace project markdown files and Python scripts, identifying line-by-line instances of `FastAPI` declarations.
- **Why Chat Alone Cannot Do This**: Chat models cannot execute ripgrep/system binaries across multi-file directories.

---

## 📖 Technical Explainer Summary

*Full 780-word essay available in [`mcp_explainer.md`](mcp_explainer.md).*

### Key Takeaways:
1. **Workflows vs. Agents**: Workflows execute hardcoded, deterministic paths (Step A $\rightarrow$ Step B $\rightarrow$ Step C). Agents operate in an autonomous loop, evaluating environment feedback and dynamically choosing which tools to invoke until a goal is reached.
2. **FL-04 Classification**: The FL-04 pipeline is a **Workflow** because its handoffs are fixed by code rather than autonomously chosen by the model.
3. **MCP Primitives**: Model Context Protocol defines **Tools** (executable actions), **Resources** (read-only context data), and **Prompts** (pre-configured templates).
4. **Agent Upgrade**: Upgrading FL-04 to an agent involves adding an MCP-driven feedback loop where the agent runs `pytest`, inspects failure logs, and self-corrects code until all tests pass.

---

## ✅ Pass / Revise Self-Audit Checklist

- [x] **Technical Explainer (600–900 words)**: 780-word essay written in own words (`mcp_explainer.md`).
- [x] **Accurate Classification**: Accurately classified FL-04 as a deterministic workflow.
- [x] **Demonstrable Tool Use**: 3 explicit tasks executed using MCP tool calls (`list_dir`, `view_file`, `grep_search`).
- [x] **3 Tasks Chat Alone Could Not Do**: File system listing, local file viewing, and ripgrep search verified.
- [x] **Concrete Agent Upgrade**: Detailed self-correction agent loop designed for FL-04.
