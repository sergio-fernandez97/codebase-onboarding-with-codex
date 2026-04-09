
# Live Session: Codebase Onboarding with Codex + MCP

# 🎯 Objective

## Goal of the Live Session

Learn how to use **Codex + MCP servers** to:

* Understand an unfamiliar repository
* Extract structured knowledge from code
* Generate explanations, diagrams, and learning paths
* Publish findings into a **visual, reusable knowledge artifact**

---

## 🧾 Expected Output

By the end of the session, you will have:

* A **structured onboarding document** (Markdown)
* Including:

  * Repository overview
  * Folder structure
  * Algorithm explanation
  * Learning path
  * Mermaid diagram
* Automatically published into **Obsidian via MCP**

---

# ⚙️ Prerequisites

## 1. System Requirements

* macOS / Linux / Windows
* Docker installed and running
* Node.js (v18+ recommended)
* VS Code (recommended)

---

## 2. Clone the Repository

```bash
git clone https://github.com/TheAlgorithms/Python.git
cd Python
```

---

## 3. Install Codex CLI

Follow official setup (already covered in your course).

---

## 4. Install Obsidian (FREE)

* Download from: [https://obsidian.md](https://obsidian.md)
* Create a **Vault** (e.g. `AI-Knowledge`)

👉 Obsidian is free with no feature limits ([Obsidian][1])

---

## 5. Install Obsidian Plugins

Inside Obsidian:

1. Enable **Community Plugins**
2. Install:

* ✅ **Obsidian Local REST API plugin**
1. Launch Obsidian & Open your Vault (or create one).
2. Click ⚙️ (bottom-left corner) **OR** Press:
```bash
Cmd + ,   (Mac)
Ctrl + ,  (Windows/Linux)
```
3. Go to **Community plugins**
4. Click **Browse** and in the search bar, type:
```bash
Local REST API
```
5. Find it (by coddingtonbear). Click **Install**. Then click **Enable**.
6. Open the Plugin Settings and Click **Local REST API**.
7. Copy into .env:
  * API Key -> `OBSIDIAN_API_KEY`
  * Host + Port (default usually: `127.0.0.1:27124`) -> `HOST` and `PORT`

  👉 You will need this for MCP config

8. Enable Non-encrypted (HTTP) Server.
---

## 6. Configure Obsidian MCP Server (Docker MCP Toolkit)

You will use:

### ✅ MCP Server Required

### 🧠 Obsidian MCP Server

* Enables:

  * Read/write notes
  * Search vault
  * Append content
  * Manage files

👉 This server allows AI agents to interact with your vault programmatically ([Awesome MCP Servers][2])

---
## 7. Add MCP Server through Docker MCP Toolkit
1. Go to docker `MCP Toolkit > Clients`. Look up `Codex` and press connect **OR** use the following command.
```bash
docker mcp client connect codex
```
2. Then go to `MCP Toolkit > My servers`. Search for the server `Obsidian` and press `Add`.

3. After adding the MCP server. Use the following command for listing the current mcp servers added.
```bash
docker mcp server ls
```
Verify you se `obsidian`. 

**OR** Add MCP Server Configuration

In your MCP client config:

```json
{
  "mcpServers": {
    "obsidian": {
      "command": "docker",
      "args": [
        "run",
        "-i",
        "--rm",
        "-e",
        "OBSIDIAN_HOST",
        "-e",
        "OBSIDIAN_API_KEY",
        "mcp/obsidian"
      ],
      "env": {
        "OBSIDIAN_HOST": "host.docker.internal",
        "OBSIDIAN_API_KEY": "YOUR_API_KEY"
      }
    }
  }
}
```

👉 The MCP server interacts with Obsidian via its REST API plugin ([Docker Hub][3])

---

# ⚙️ Agent Configuration

Before starting the live exercise, configure how Codex should behave for this repository.

Codex supports configuration in a `.codex` directory, and this can be set up in two ways:

* Project-level: `./.codex/`
* Global-level: `~/.codex/`

For this workshop, prefer a project-level `./.codex/` setup so the repository contains its own agent instructions, skills, and MCP-related configuration. Then add an `AGENTS.md` file at the repository root to define how the agent should work in this specific codebase.

---

# 🚀 Step-by-Step Live Session

---

# 🔹 PART 1 — Start Codex
```bash
cd ..
```

```bash
codex
```
Create a [`AGENTS.md`](https://agents.md) file through the following prompt inside codex
```
Create a brief AGENTS.md file, I want the agent to analyze the repository ./Python for in order to create onboarding documentation. 
Every requested finding must be saved at ./findings in markdown format with a meaningful name. Whenever the user refers to a repo it means ./Python if he's not refering explicitly to another one. 
```

---

# 🔹 PART 2 — Understand the Repository

### Step 1 — Explain the repo

```text
› Explain the repository ./Python:
  - What it does
  - Structure
  - Key modules
  - Where to start 
```

---

### Step 2 — Explore structure

```text
What are the main folders and what do they contain?
```

---

### Step 3 — Identify entry point

```text
Where should a beginner start in this repository?
```

---

# 🔹 PART 3 — Deep Dive into Code

---

### Step 4 — Select a module

```text
Show me a simple sorting algorithm from this repo (./Python)
```

---

### Step 5 — Explain the code

```text
Explain the algorithm step by step
```

---

### Step 6 — Analyze complexity

```text
What is the time complexity?
```

---

### Step 7 — Suggest improvements

```text
How can this be improved?
```

---

---

# 🔹 PART 4 — Generate Knowledge Artifact

---

### Step 8 — Create structured document

```text
Create a structured onboarding document (named ONBOARDING.md) explaining this repo including:
- Overview
- Folder structure
- Key modules
- Example explanation
- Learning path
```

---

### Step 9 — Add diagram

```text
Add a Mermaid diagram showing repo structure
```

---

### Step 12 — Add onboarding guide

```text
Add:
- Where to start
- First files to read
- Suggested exercises
```

---

# 🔹 PART 5 — Publish with MCP (🔥 KEY STEP)

---

### Step 13 — Publish to Obsidian

```text
Use MCP to create a file:

Path: AI-Knowledge/TheAlgorithms-Onboarding.md

Content: (generated document)
```

---

### What happens here:

* Codex generates markdown
* MCP writes file into Obsidian
* Obsidian renders it visually

👉 MCP enables secure read/write operations over your vault ([Awesome MCP Servers][2])

---

# 🔹 PART 6 — Use Skill
This is brief overview of skills for OpenAI Codex.

>
Use agent skills to extend Codex with task-specific capabilities. A skill packages instructions, resources, and optional scripts so Codex can follow a workflow reliably. You can share skills across teams or with the community. — Open AI
>


Read the [documentation](https://developers.openai.com/codex/skills/) for further information.

* Other sources: [YouTube](https://www.youtube.com/watch?v=en0It1zBjpw).

### QuickStart 
1. Execute `codex` and then press the command `\skills`.
2. List the available skills
```
Skill Creator -> $skill-creator
Skill Installer -> $skill-installer
```

---

### Step 14 — Use the native skill to create a new skill

Inside Codex, use the built-in skill creation flow to generate a reusable skill:

```text
Use the native skill-creator skill to create a new skill named repo-onboarding-publisher.

The skill must:
- Analyze the repository
- Summarize the structure
- Select one beginner-friendly example
- Explain the example step by step
- Generate a Mermaid diagram
- Create an onboarding document in markdown
- Publish the onboarding document to Obsidian via MCP

Assume that when I mention "the repo" I mean ./Python.
```

---

### Step 15 — Review the generated skill

Make sure the generated skill clearly captures the workflow and expected output:

```yaml
name: repo-onboarding-publisher

steps:
  - Analyze repository
  - Summarize structure
  - Select key example
  - Explain code
  - Generate diagram
  - Create onboarding doc
  - Publish via MCP
```

---

### Step 16 — Refine the skill behavior

Ask Codex to improve the generated skill so it is specific and reusable:

```text
Refine the repo-onboarding-publisher skill so it always:
- Reads the repo from ./Python unless another path is provided
- Produces a markdown onboarding document
- Includes overview, structure, key modules, beginner starting point, example explanation, learning path, and Mermaid diagram
- Publishes the final document into Obsidian
```

---

### Step 17 — Use the new skill

Execute the skill directly:

```text
Use repo-onboarding-publisher skill
```

---

### Step 18 — Verify the published result

Confirm that the skill completed the full workflow:

```text
Verify that the onboarding document was published in Obsidian and tell me the final file path.
```

### Step 19 - Install an external skill 

1. Install the skill [$agent-skill-evaluator](https://github.com/JeredBlu/eval-marketplace/tree/main)
2. Evalute the skill `$repo-onboarding-publisher` with `$agent-skill-evaluator`.

### Step 20 - Test our skill with a different repo

---

# 🧠 Conclusions

---

## 🚀 Key Learnings

* Codex is not just for coding — it is for:

  * Understanding
  * Structuring
  * Documenting

---

## 🔥 Most Important Insight

> Understanding code is not enough —
> You must **capture and share that understanding**

---

## 🧩 What You Built

You created:

* A **knowledge pipeline**

```text
Codebase → Codex → Structured Knowledge → MCP → Obsidian
```

---

## ⚡ Why This Matters

This workflow enables:

* Faster onboarding
* Reusable knowledge
* AI-assisted documentation
* Scalable team learning

---

# 📘 Weekly Practical Assignment

## Objective

Build your own `repo-onboarding-publisher` skill using the native skill flow in Codex (AI-generated is recommended), then use it with a different repository to produce and publish a new onboarding document.

---

## Instructions

1. Choose a repository different from `./Python`.
2. Configure and add Obsidian MCP server for codex (review the README.md file from the live session).
3. Add an `AGENTS.md` file that defines how the agent should work with that repo.
4. Use the native skill creation flow to build your own `repo-onboarding-publisher` skill.
5. Run the skill against the new repository.
6. Publish the resulting onboarding document to Obsidian.

---

## Deliverables

* A GitHub repository containing the `.codex` configuration, the `AGENTS.md` file, and the `README.md` file cleary stating which repository was used and mentioning how to used the custom skill. 
* A screenshot proving that the onboarding document was published in Obsidian.

---

## 🧠 Final Thought

> Codex is not just an assistant.
> It is a **knowledge generator connected to your system**.

---

[1]: https://obsidian.md/pricing?utm_source=chatgpt.com "Pricing"
[2]: https://mcpservers.org/servers/cyanheads/obsidian-mcp-server?utm_source=chatgpt.com "Obsidian MCP Server"
[3]: https://hub.docker.com/r/mcp/obsidian?utm_source=chatgpt.com "mcp/obsidian - Docker Image"
