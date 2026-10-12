# AgentLTL

**Procedural rules for tool-using LLM agents, checked before each tool call runs.**

When an agent works through a task it calls tools in some order. AgentLTL lets you state
constraints over that order, such as *run the tests before pushing* or *never force-push*, as
First-Order Linear Temporal Logic (FOLTL) formulas. It then verifies them against the agent's
tool-call trace, after a run or live, blocking or warning on a call before it executes.

📖 **Documentation: [agentltl.github.io](https://agentltl.github.io)**

## Repositories

| | |
|---|---|
| [**AgentLTL**](https://github.com/AgentLTL/AgentLTL) | The FOLTL engine: post-hoc verification, runtime enforcement, compliance scoring. |
| [**agentltl-coding**](https://github.com/AgentLTL/agentltl-coding) | Rules for coding agents: the `AGENTLTL.yaml` language, a library of tested rules, and a guard any harness can call. |
| [**cli-to-tools**](https://github.com/AgentLTL/cli-to-tools) | Translates shell command lines into ordered, structured tool calls, so a single `bash` tool can be constrained too. |

### Coding-agent plugins

Enforce your `AGENTLTL.yaml` rules on every tool call, shell commands included:

- [Claude Code](https://github.com/AgentLTL/agentltl-claude-code)
- [Codex](https://github.com/AgentLTL/agentltl-codex)
- [GitHub Copilot CLI](https://github.com/AgentLTL/agentltl-copilot-cli)
- [Mistral Vibe](https://github.com/AgentLTL/agentltl-mistral-vibe)

## Install in your agent

Paste the line for your agent into it, and it sets the plugin up and helps you pick rules:

**Claude Code**
```
Set up the AgentLTL plugin for me by following https://raw.githubusercontent.com/AgentLTL/agentltl-claude-code/main/SETUP.md
```

**Codex**
```
Set up the AgentLTL plugin for me by following https://raw.githubusercontent.com/AgentLTL/agentltl-codex/main/SETUP.md
```

**GitHub Copilot CLI**
```
Set up the AgentLTL plugin for me by following https://raw.githubusercontent.com/AgentLTL/agentltl-copilot-cli/main/SETUP.md
```

**Mistral Vibe**
```
Set up the AgentLTL plugin for me by following https://raw.githubusercontent.com/AgentLTL/agentltl-mistral-vibe/main/SETUP.md
```

## Python packages

All three are on PyPI:

```bash
pip install agentltl          # the FOLTL engine
pip install cli-to-tools      # shell command lines to structured tool calls
pip install agentltl-coding   # the AGENTLTL.yaml rules and guard (pulls in the other two)
```

## A rule in a few lines

```yaml
rules:
  - id: tests-before-push
    before: {first: pytest, then: git_push, since: [Edit, Write]}
    why: CI is slow; run the tests locally first.
    mode: warn
use: [no-force-push, protect-secret-files]   # from the rule library
```
