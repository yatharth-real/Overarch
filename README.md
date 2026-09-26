<div align="center">

# ◆ OVERARCH

**The Learning Agent for Autonomous Software Engineering.**

[![npm version](https://img.shields.io/npm/v/overarch?color=56c2ff&label=npm&style=flat-square)](https://www.npmjs.com/package/overarch)
[![npm downloads](https://img.shields.io/npm/dm/overarch?color=94a9d6&style=flat-square)](https://www.npmjs.com/package/overarch)
[![license](https://img.shields.io/badge/license-MIT-5c1122?style=flat-square)](./LICENSE)
[![node](https://img.shields.io/badge/node-%E2%89%A520-081842?style=flat-square)](https://nodejs.org)

```
npm install -g overarch
```

</div>

---

Most AI coding agents generate code *inside* your project. Overarch is built to learn the *structure* of your project first — the conventions, the file layout, the constraints — and act from there. It runs entirely in your terminal, reasons over your actual codebase, executes real tools and commands, and carries a task through from intent to a verified, working change.

```text
$ overarch
> find the failing tests, identify the root causes, and fix them
```

---

## Why Overarch

| | |
|---|---|
| **Terminal-native** | No IDE lock-in. Works over SSH, in CI, in a tmux pane, anywhere a shell runs. |
| **Project-aware** | Builds an understanding of your codebase's structure, not just its text. |
| **Human-controlled** | Every risky action is gated by an explicit, fail-closed policy engine — see [CCHCFAI](#cchcfai--human-control-framework). |
| **Provider-agnostic** | Route to any model through OpenRouter or your own provider config. |
| **Extensible** | Teach it new workflows permanently with [Skills](#skills). |

<br>

## Overarch vs. The Field

<div align="center">

| | **Overarch** | Claude Code | Cursor | Aider |
|---|:---:|:---:|:---:|:---:|
| **Interface** | Terminal-native agent | Terminal-native agent | IDE (fork of VS Code) | Terminal-native agent |
| **Runs where code lives** | ✅ Any shell, SSH, CI | ✅ Any shell, SSH, CI | ❌ Requires the Cursor editor | ✅ Any shell, SSH, CI |
| **Explicit human-control layer** | ✅ CCHCFAI risk-tiered policy engine (R0–R5) | ⚠️ Permission prompts, less granular | ⚠️ Inline diff approval | ⚠️ Confirm-before-edit only |
| **Fail-closed on unknown actions** | ✅ Unregistered actions default to `DENY` | ❌ Not a core guarantee | ❌ Not a core guarantee | ❌ Not a core guarantee |
| **Model routing** | ✅ Configurable via OpenRouter, multi-provider | ❌ Anthropic models only | ⚠️ Fixed set of hosted models | ✅ Multi-provider |
| **Skill system** | ✅ User-authored, extends agent without core changes | ⚠️ Limited custom instructions | ❌ No equivalent | ❌ No equivalent |
| **Response QC layer** | ✅ CCSS correctness/relevance checks | ⚠️ Implicit | ❌ Not exposed | ❌ Not exposed |
| **Best fit for** | Engineers who want an agent that respects project structure *and* explicit control boundaries | General-purpose coding, tightest Claude integration | Developers who want AI embedded in a full IDE | Fast, minimal git-based pair programming |

</div>

> Overarch's differentiation isn't "another chat wrapper around a terminal" — it's the combination of project-structure learning *and* an explicit, auditable control layer most agents leave implicit.

<br>

## Install

**Requirements:** Node.js 20+, and an LLM provider/API key supported by your Overarch config.

<table>
<tr><td><b>npm</b></td><td>

```bash
npm install -g overarch
```

</td></tr>
<tr><td><b>pnpm</b></td><td>

```bash
pnpm add -g overarch
```

</td></tr>
<tr><td><b>No install (one-off run)</b></td><td>

```bash
npx overarch
```

</td></tr>
</table>

Then, from any project directory:

```bash
cd my-project
overarch
```

<br>

## Quick Start

```text
$ overarch
> inspect this project and explain its architecture
```

```text
$ overarch
> find the failing tests, identify the root causes, and fix them
```

Overarch reads the project it's launched in as its working context — no separate indexing step, no config file required to get started.

<br>

## Core Concepts

<details>
<summary><b>Agent</b> — an engineering loop, not a text generator</summary>
<br>

Overarch operates on a fixed cycle: **Understand → Plan → Act → Verify → Learn**. It inspects the project, reasons about the change it intends to make, executes it through real tools, and verifies the result before considering the task complete.

</details>

<details>
<summary><b>Skills</b> — teach Overarch new workflows permanently</summary>
<br>

Skills are user-authored extensions that give Overarch specialized instructions and procedures for a given workflow, without modifying the core agent. Once added, a skill is available in every future session.

</details>

<details>
<summary id="cchcfai--human-control-framework"><b>CCHCFAI</b> — Creative Customs Human Control for AI</summary>
<br>

The framework governing what Overarch is allowed to do without asking first.

- **Action states:** `SUGGEST`, `REQUEST_APPROVAL`, `EXECUTE`, `DENY`, `ESCALATE`, `STOP`
- **Capabilities:** `READ_FILES`, `WRITE_FILES`, `DELETE_FILES`, `EXECUTE_COMMANDS`, `NETWORK_ACCESS`, `BROWSER_ACCESS`, `APPLICATION_CONTROL`, and more
- **Risk levels:** `R0` (informational) through `R5` (prohibited destructive actions, e.g. `rm -rf /`, `format`)
- **Fail-closed default:** any action Overarch doesn't recognize defaults to `DENY` — nothing runs by ambiguity
- **Emergency stop:** `SIGINT`/`SIGTERM` immediately terminates every spawned child process

</details>

<details>
<summary><b>CCSS</b> — Creative Customs Smart Skill</summary>
<br>

An orchestration layer that checks Overarch's own output for correctness, relevance, reasoning quality, completeness, practical usefulness, and communication efficiency before it's surfaced to you.

</details>

<details>
<summary><b>Project Sessions</b> — the directory is the context</summary>
<br>

Overarch operates from whatever directory it's launched in. `cd` into a project, run `overarch`, and the agent's working context is that project — no separate registration step.

</details>

<br>

## Commands

```text
/help
```

shows every available command, categorized by session control, configuration, skills, and agent operation.

<br>

## Models

Overarch routes to models through a configurable provider setup. By default it uses OpenRouter's automatic routing; you can point it at your own supported provider/model configuration instead.

<br>

## Development

```bash
git clone <repo-url>
cd overarch
npm install     # install dependencies
npm run build   # build
npm run dev     # run in development
npm test        # run the test suite
```

<br>

## Project

Overarch is built by **Yatharth Roy** under **The Thursday AI Company**, New Delhi.

## License

Released under the [MIT License](./LICENSE).

</div>
