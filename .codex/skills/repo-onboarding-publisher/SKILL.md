---
name: repo-onboarding-publisher
description: Analyze a repository and produce onboarding documentation for new engineers or learners. Use when Codex needs to inspect a codebase, summarize its structure and key modules, choose one beginner-friendly example, explain that example step by step, generate a Mermaid diagram of the repo structure, write the onboarding document in Markdown, and publish the final document to Obsidian via MCP.
---

# Repo Onboarding Publisher

## Overview

Create a concise onboarding document for a repository, save the Markdown locally, and publish the same content to Obsidian.

Prefer a practical explanation over an exhaustive audit. The document should help a new reader understand what the repo is, how it is organized, what files matter, and where to start.

## Workflow

1. Determine the target repository.
If the user gives a path, use it. If the surrounding project defines a default repo convention, follow it. Otherwise, use the current project root.

2. Inspect the repository before writing.
Read the top-level files and structure first. Prefer fast discovery commands such as:
- `rg --files <repo>`
- `find <repo> -maxdepth 2 -type d | sort`
- `sed -n '1,220p' <repo>/README.md`
- `sed -n '1,260p' <repo>/pyproject.toml`
- `sed -n '1,260p' <repo>/package.json`
- `sed -n '1,260p' <repo>/.github/workflows/*.yml`

3. Identify the document anchors.
At minimum, gather enough context to explain:
- what the repo does
- how the top-level folders are organized
- which files define contributor or runtime expectations
- which example is easiest for a beginner to follow

4. Select one beginner-friendly example.
Prefer an example that is:
- small
- self-contained
- readable without heavy setup
- representative of repo style

Avoid examples that depend on large datasets, complex frameworks, external services, or advanced domain knowledge unless the repo is entirely centered on those.

5. Explain the example step by step.
Do not just paste code. Explain the control flow or data flow in a way a new engineer can follow.

6. Generate a Mermaid diagram.
Create a simple repo-structure diagram that highlights the repo root and the major files or folders that matter for onboarding. Keep it compact.

7. Write the onboarding document in Markdown.
Use the section structure from `references/onboarding-template.md`.

8. Save the local Markdown file.
If the user gives a filename, use it. Otherwise, prefer `./findings/ONBOARDING.md`.

9. Publish the same content to Obsidian via MCP.
If the user gives an Obsidian path, use it. Otherwise, choose a sensible note path that matches the repo name or onboarding topic.
Before publishing, check whether the note already exists.
- If it does not exist, create it with `obsidian_append_content`.
- If it exists and already matches, do nothing.
- If it exists and differs, replace it exactly instead of appending duplicate content. Use the available Obsidian MCP operations needed to keep the note content in sync.

## Output Contract

The onboarding document must contain:
- `Overview`
- `Folder Structure`
- `Key Modules`
- `Example Explanation`
- `Learning Path`

The `Folder Structure` section must include one Mermaid diagram.

The final Markdown should be concise but complete enough that a new contributor can decide where to start in under five minutes.

## Obsidian Publishing

When publishing through MCP:
- verify whether the target note already exists
- avoid duplicate appends
- keep the Obsidian note content identical to the local Markdown file
- report the final Obsidian path back to the user

## References

- Read `references/onboarding-template.md` before drafting the final document if you need a reminder of the expected structure and tone.
