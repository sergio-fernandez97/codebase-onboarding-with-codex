# Security Assessment: repo-onboarding-publisher

## Executive Summary

- Overall Risk Level: `USE WITH CAUTION`
- Source: Local project skill at `./.codex/skills/repo-onboarding-publisher`
- Evaluation Date: 2026-04-08
- Evaluator: Codex using `agent-skill-evaluator`
- Critical Findings: No prompt injection strings, hidden Unicode instructions, executable scripts, or exfiltration logic were found. The skill does request publishing to Obsidian via MCP, which is a real external side effect and should remain user-directed.
- Recommendation: Safe for local use in its current form. Use with normal review because it can write local Markdown and publish notes to Obsidian.

## Source & Provenance

This skill is local to the current project, not downloaded from an unknown third-party source.

Evidence:
- Skill path: `./.codex/skills/repo-onboarding-publisher`
- Files are currently uncommitted local changes in this repo.
- Local git user is `sergio-fernandez97`.

Assessment:
- Strong local provenance for immediate use.
- Weak external reputation signal because the skill is not published or independently reviewed.

## Skill Structure Overview

Observed file structure:

- `SKILL.md`
- `agents/openai.yaml`
- `references/onboarding-template.md`

Notably absent:
- no `scripts/`
- no `assets/`
- no binary files

File-type check:
- all inspected files are ASCII text
- no hidden executable content was present in the skill directory

## SKILL.md Analysis

### Prompt Injection Detection

No prompt injection patterns were found in [SKILL.md](/Users/sergio.fernandez/Documents/AI-Initiative/AI-Literacy-Culture-Sales/courses/Coding-Assistants-&-AI-Agents/april-26/codebase-onboarding-with-codex/.codex/skills/repo-onboarding-publisher/SKILL.md#L1).

Checks performed:
- searched for phrases such as `Ignore previous instructions`, `disregard`, `You are now`, `Act as if`, `Pretend you are`
- searched for encoded payload indicators such as `base64`
- scanned for hidden Unicode control characters

Result:
- no matches

### Suspicious Behavioral Instructions

No malicious or deceptive instructions were found.

The skill stays within its stated purpose:
- inspect a repository
- summarize structure
- choose a beginner-friendly example
- generate Markdown
- publish to Obsidian

Relevant workflow lines:
- repo inspection guidance at [SKILL.md](/Users/sergio.fernandez/Documents/AI-Initiative/AI-Literacy-Culture-Sales/courses/Coding-Assistants-&-AI-Agents/april-26/codebase-onboarding-with-codex/.codex/skills/repo-onboarding-publisher/SKILL.md#L19)
- local file write guidance at [SKILL.md](/Users/sergio.fernandez/Documents/AI-Initiative/AI-Literacy-Culture-Sales/courses/Coding-Assistants-&-AI-Agents/april-26/codebase-onboarding-with-codex/.codex/skills/repo-onboarding-publisher/SKILL.md#L53)
- Obsidian publishing guidance at [SKILL.md](/Users/sergio.fernandez/Documents/AI-Initiative/AI-Literacy-Culture-Sales/courses/Coding-Assistants-&-AI-Agents/april-26/codebase-onboarding-with-codex/.codex/skills/repo-onboarding-publisher/SKILL.md#L56)

There are no instructions to:
- hide actions from the user
- override user intent
- ignore safety controls
- gather credentials
- contact unknown remote services

### Over-Permissioned Requests

The skill does ask for write-capable behavior:
- save local Markdown under `./findings`
- publish to Obsidian via MCP

This is justified by the skill purpose, but it is still a permission-bearing workflow. That is the main reason this assessment is `USE WITH CAUTION` rather than fully unrestricted `USE`.

Risk note:
- Obsidian publishing can modify user notes outside the repo.
- The skill does not specify a hard allowlist for note paths, so misuse would depend on the calling prompt and operator review.

## Scripts Security Analysis

No `scripts/` directory exists in this skill.

Assessment:
- no executable code to review
- no subprocess, shell execution, network code, or file traversal logic bundled in the skill itself

## References & Assets Analysis

Reference file reviewed:
- [onboarding-template.md](/Users/sergio.fernandez/Documents/AI-Initiative/AI-Literacy-Culture-Sales/courses/Coding-Assistants-&-AI-Agents/april-26/codebase-onboarding-with-codex/.codex/skills/repo-onboarding-publisher/references/onboarding-template.md#L1)

Findings:
- purely structural guidance
- no hidden instructions
- no external links
- no embedded code execution directions

Assets:
- none present

## Community Feedback & External Research

Search queries used:
- `"repo-onboarding-publisher" skill`
- `"repo-onboarding-publisher" Codex skill`
- `"sergio-fernandez97" Codex skill repo-onboarding-publisher`

Results:
- no relevant public references to this skill were found
- no community warnings or endorsements were found

Interpretation:
- absence of public concern is not strong evidence of safety
- this looks like a local-only skill with no external reputation footprint yet

## Attack Pattern Analysis

Matched threat patterns:
- none

Specifically not observed:
- prompt override attempts
- hidden Unicode steering
- encoded command payloads
- external URL beacons
- credential prompts
- bundled executable payloads
- persistence or self-modification behavior

## Risk Assessment

### Detailed Scoring

| Dimension | Score (0-100) | Justification |
|-----------|---------------|--------------|
| Prompt Injection | 94 | No override strings, hidden control characters, or concealed directives found in the text files. |
| Code Safety | 98 | No executable scripts or binary assets are included. |
| Data Privacy | 78 | The skill can publish content to Obsidian, which is a legitimate side effect but still modifies user-owned data. |
| Source Trust | 72 | Local project ownership is good, but there is no external review or release history. |
| Functionality | 88 | Behavior is consistent with the stated onboarding purpose and does not claim unrelated capabilities. |
| **OVERALL RATING** | **86** | Safe in content and structure, with normal caution required because it writes files and publishes to Obsidian. |

### Threat Summary

1. Low: Obsidian note writes are external to the repo and could affect unintended notes if the path is mis-specified.
2. Low: The skill does not enforce a strict path policy for publishing targets.
3. Informational: No independent public trust signal exists because the skill appears local and unpublished.

### False Positive Analysis

Potential false positive considered:
- The presence of MCP publishing instructions could look suspicious because it writes outside the repo.

Why it was not treated as malicious:
- Publishing is explicitly aligned with the user-requested skill purpose.
- No deceptive behavior or hidden transmission pattern accompanies it.
- The skill states the action directly in plain text at [SKILL.md](/Users/sergio.fernandez/Documents/AI-Initiative/AI-Literacy-Culture-Sales/courses/Coding-Assistants-&-AI-Agents/april-26/codebase-onboarding-with-codex/.codex/skills/repo-onboarding-publisher/SKILL.md#L56).

## Final Verdict

**Recommendation**: `USE`

**Reasoning**: The skill contains only plain-text instructions and one plain-text reference file. It shows no signs of prompt injection, hidden instructions, malicious code, or covert exfiltration. Its only material risk is that it intentionally writes output locally and publishes to Obsidian, which is expected behavior for this skill class.

**Specific Concerns**:
- review the requested Obsidian path before publishing
- keep the user in the loop for note replacement behavior

**Safe Use Cases**:
- local repository onboarding generation
- internal documentation workflows
- controlled publication of generated notes to known Obsidian paths

**Alternative Skills**:
- none required based on this assessment

## Evaluation Limitations

- No public package or repository history was available for reputation scoring.
- Community validation produced no relevant public results for the exact skill name.
- The assessment evaluated the current local files only.

## Evidence Appendix

Key files reviewed:
- [SKILL.md](/Users/sergio.fernandez/Documents/AI-Initiative/AI-Literacy-Culture-Sales/courses/Coding-Assistants-&-AI-Agents/april-26/codebase-onboarding-with-codex/.codex/skills/repo-onboarding-publisher/SKILL.md#L1)
- [openai.yaml](/Users/sergio.fernandez/Documents/AI-Initiative/AI-Literacy-Culture-Sales/courses/Coding-Assistants-&-AI-Agents/april-26/codebase-onboarding-with-codex/.codex/skills/repo-onboarding-publisher/agents/openai.yaml#L1)
- [onboarding-template.md](/Users/sergio.fernandez/Documents/AI-Initiative/AI-Literacy-Culture-Sales/courses/Coding-Assistants-&-AI-Agents/april-26/codebase-onboarding-with-codex/.codex/skills/repo-onboarding-publisher/references/onboarding-template.md#L1)

Key behavioral lines:
- target repo selection at [SKILL.md](/Users/sergio.fernandez/Documents/AI-Initiative/AI-Literacy-Culture-Sales/courses/Coding-Assistants-&-AI-Agents/april-26/codebase-onboarding-with-codex/.codex/skills/repo-onboarding-publisher/SKILL.md#L16)
- local output file guidance at [SKILL.md](/Users/sergio.fernandez/Documents/AI-Initiative/AI-Literacy-Culture-Sales/courses/Coding-Assistants-&-AI-Agents/april-26/codebase-onboarding-with-codex/.codex/skills/repo-onboarding-publisher/SKILL.md#L53)
- Obsidian publishing guidance at [SKILL.md](/Users/sergio.fernandez/Documents/AI-Initiative/AI-Literacy-Culture-Sales/courses/Coding-Assistants-&-AI-Agents/april-26/codebase-onboarding-with-codex/.codex/skills/repo-onboarding-publisher/SKILL.md#L56)
