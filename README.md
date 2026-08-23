<div align="center">
  <img src="assets/hero.svg" alt="Nipun Kalsotra — I build autonomous systems that can prove what they did" width="100%">
</div>

<div align="center">

<a href="mailto:kalsotranipun@gmail.com"><img src="https://img.shields.io/badge/Email-kalsotranipun@gmail.com-00D9FF?style=flat-square&logo=gmail&logoColor=white&labelColor=0d1117"></a>
<a href="https://github.com/nipunkalsotra?tab=repositories"><img src="https://img.shields.io/badge/Repositories-15_public-836EF9?style=flat-square&logo=github&logoColor=white&labelColor=0d1117"></a>
<img src="https://img.shields.io/badge/Focus-Multi--Agent_Systems-00D9FF?style=flat-square&labelColor=0d1117">
<img src="https://img.shields.io/badge/Building_since-Aug_2025-836EF9?style=flat-square&labelColor=0d1117">

</div>

<br>

## The thesis

Autonomous systems are being handed real authority — approving claims, patching production, routing work — and almost none of them can **prove** what they did. The reasoning is a black box, the logs are mutable, and "trust me" is the entire audit story.

Every serious thing I've built in the last twelve months attacks that from a different angle: writing agent decisions to an immutable ledger, hash-chaining a self-healing system's state transitions, forcing adversarial verification before a verdict, sandboxing an AI that rewrites your code. Different domains, one obsession — **make the machine produce receipts.**

I'm a BSc CS student. I learn by building the hard version.

<br>

## Receipts

> Commit counts below are **mine specifically**, not repo totals. Team projects are marked.

<table>
<tr>
<td width="50%" valign="top">

### ⛓️ [TrustChain](https://github.com/nipunkalsotra/TrustChain)
**Every AI agent decision, permanently on-chain.**

A 4-agent LangGraph pipeline where each decision, tool call, and handoff is written as a transaction on the Monad blockchain. Click any step in the live feed → jump to its transaction on the explorer.

`3 Solidity contracts deployed` · `SSE live streaming` · `MCP tool servers` · `k6 load tests` · `gitleaks + pre-commit + semantic-release`

<sub>**Python · TypeScript · Solidity · Next.js 14 · FastAPI · LangGraph · web3.py · Groq**</sub>
<br><sub>👥 Team of 2 · 28 commits mine</sub>

</td>
<td width="50%" valign="top">

### 🛡️ [NeuralGuard](https://github.com/nipunkalsotra/NeuralGaurd)
**A workflow orchestrator that heals itself.**

Detects a stuck agent in under a second, diagnoses root cause, generates *and verifies* a patch, reroutes around the failure — zero humans. Every state transition lands in an append-only **SHA-256 hash-chained** audit log: mutate one record and every hash after it fails.

The frontend ships a from-scratch **TypeScript port of the entire orchestration core**, so the deployed site runs a real healing cycle with no backend at all.

`7-state FSM` · `4 async agents` · `circuit breakers` · `cosine-similarity loop detection @ 0.92`

<sub>**Python 3.14 · FastAPI · React 19 · Vite · WebSockets · Docker**</sub>
<br><sub>👥 Team of 2 · 48 commits mine · top contributor</sub>

</td>
</tr>
<tr>
<td width="50%" valign="top">

### 🔍 [TruthFrame](https://github.com/nipunkalsotra/TruthFrame)
**Six-stage claim verifier, built in 24 hours.**

Decides whether a photo *supports*, *contradicts*, or *can't settle* a damage claim. OpenCV pre-screening kills wasted API calls, a token-bucket limiter saturates the quota, and risk-adaptive routing scales compute to claim complexity — with an adversarial multi-agent pass reserved for the expensive edge cases.

`HackerRank Orchestrate 2026` · `self-correcting schema loop → 100% compliance`

<sub>**Python · Gemini Vision · Groq LLaMA 3 · OpenCV · asyncio**</sub>
<br><sub>👥 Hackathon team · 13 commits mine</sub>

</td>
<td width="50%" valign="top">

### 🍽️ [Mini Restaurant OS](https://github.com/nipunkalsotra/mini-Restaurant-OS)
**Full-stack, shipped, and actually live.**

Menu → cart → customer → order lifecycle → billing → payment → sales tracking. The whole loop, deployed across three providers and running in production.

[**→ mini-restaurant-os.vercel.app**](https://mini-restaurant-os.vercel.app)

<sub>**React · FastAPI · PostgreSQL · SQLAlchemy · Vercel · Render · Neon**</sub>
<br><sub>🧍 Solo · 57 commits — my largest solo build</sub>

</td>
</tr>
</table>

<details>
<summary><b>Four more worth opening →</b></summary>

<br>

| Project | The interesting part | Stack |
|---|---|---|
| 🐚 [**Custom POSIX Shell**](https://github.com/nipunkalsotra/CodeCrafters-OS-Shell) | A Unix shell from scratch — quote-aware parsing, redirection, pipelines, background jobs, builtins. No shell library, just syscalls and a parser. | Java 26 · Maven |
| 🧠 [**IdeaGuard**](https://github.com/nipunkalsotra/Local-AI-Debugging-Sandbox) | Autonomous debugger that runs **fully offline**. Catches a crash, spins an ephemeral Docker container capped at 512 MB with **no internet**, and loops `run → crash → patch → verify` using a local 1.5B model. <br>🏆 *Winner — "Engineering Depth" challenge* | Python · Ollama · Docker · Rich TUI |
| 🔀 [**Dynamic ETL Pipeline**](https://github.com/nipunkalsotra/Dynamic-ETL-Pipeline) | Schema-drift-tolerant ETL — the schema manager adapts to changing source shapes instead of crashing on them. | Python |
| ✍️ [**BlogForge AI**](https://github.com/nipunkalsotra/BlogForge-AI) | LLM content generation pipeline, notebook-first. | Jupyter · Python |

**Also in flight:** [OmniTrace](https://github.com/Shreshtha280407/OmniTrace) — a multimodal evidence fabric for RAG. Video, audio, image and PDF ingested into MongoDB Atlas, linked across modalities with typed timestamped relationships, retrieved as **evidence bundles instead of isolated chunks**. Phases P0–P8 complete: ASR, OCR, entity enrichment, RRF retrieval, grounded generation with validators.

</details>

<br>

## The pattern underneath

Look at four of these side by side and the same skeleton keeps showing up. I didn't plan that — I noticed it afterward, and now I build to it deliberately.

```mermaid
flowchart LR
    IN["Input<br/><i>claim · task · fault</i>"] --> PRE

    subgraph CHEAP["Cheap deterministic filter"]
      PRE["OpenCV pre-screen<br/>cosine similarity<br/>schema check"]
    end

    PRE -->|"passes"| ROUTE{"Risk / confidence<br/>routing"}
    PRE -->|"rejected early"| DONE

    ROUTE -->|"low risk"| FAST["Single fast agent<br/><i>cheap model</i>"]
    ROUTE -->|"high risk"| ADV["Adversarial multi-agent<br/><i>expensive, verified</i>"]
    ROUTE -->|"below threshold"| HUMAN["Escalate to human<br/><i>no guessing</i>"]

    FAST --> VERIFY
    ADV --> VERIFY

    VERIFY{"Self-verify"} -->|"fail"| ADV
    VERIFY -->|"pass"| LEDGER[("Tamper-evident record<br/><i>hash chain · on-chain tx</i>")]

    LEDGER --> DONE["Output + proof"]

    style CHEAP fill:#0d1424,stroke:#00D9FF,color:#cfe9ff
    style LEDGER fill:#1a1233,stroke:#836EF9,color:#e8ddff
    style HUMAN fill:#2a1a1a,stroke:#ff8c69,color:#ffd9cc
    style DONE fill:#0d1424,stroke:#00D9FF,color:#cfe9ff
```

Four rules I keep landing on:

1. **Spend the cheap check first.** OpenCV before a vision model. Cosine similarity before an LLM diagnosis. Most work shouldn't reach the expensive path.
2. **Route by risk, not uniformly.** A trivial case and a high-stakes case should not cost the same.
3. **Below the confidence threshold, escalate — don't retry.** A retry loop on a confused model is just an expensive way to stay wrong.
4. **Nothing is finished until it's recorded somewhere that can't be quietly edited.**

<br>

## Twelve months

<div align="center">
  <img src="assets/timeline.svg" alt="Trajectory from a 724-byte HTML page to multi-agent verifiable systems" width="100%">
</div>

<div align="center">
<sub>First commit: <b>August 2025</b> — a dictionary lookup page, 724 bytes of HTML.<br>
Twelve months later: hash-chained orchestrators and agent decisions committed to a blockchain.</sub>
</div>

<br>

## Stack

I've grouped these by what I actually reach for, not by what I've once installed.

<table>
<tr><td><b>Systems I reach for first</b></td><td>

`Python` `TypeScript` `FastAPI` `React` `Next.js` `PostgreSQL` `Docker`

</td></tr>
<tr><td><b>Agents & LLM orchestration</b></td><td>

`LangGraph` `Groq` `Gemini Vision` `Ollama` `MCP servers` `asyncio` `token-bucket rate limiting`

</td></tr>
<tr><td><b>Verifiability layer</b></td><td>

`Solidity` `web3.py` `Monad` `SHA-256 hash chains` `append-only audit logs`

</td></tr>
<tr><td><b>Lower level / for the understanding</b></td><td>

`Java` `C` `Linux syscalls` `shell scripting` `POSIX process management`

</td></tr>
<tr><td><b>Around the code</b></td><td>

`k6` `pre-commit` `gitleaks` `semantic-release` `SQLAlchemy` `Vite` `WebSockets` `SSE`

</td></tr>
</table>

<br>

## By the numbers

<div align="center">
  <img src="assets/stats.svg" alt="183 commits authored across 15 public repositories, 4 multi-agent systems, 12 months building" width="100%">
</div>

<div align="center">
<sub>Commit count is <b>mine specifically</b> — 183 of the 266 across these repos. Language mix measured by bytes.</sub>
</div>

<br>

## What I'm after

I want to work on systems where correctness is checkable rather than asserted — agent infrastructure, developer tooling, distributed backends, anything where "how do you know it worked?" has a real answer.

I'm most useful on problems that are slightly too hard for me at the start. That's been the pattern for twelve months and it hasn't stopped working.

<div align="center">
<br>

**[📬 kalsotranipun@gmail.com](mailto:kalsotranipun@gmail.com)** · **[💻 github.com/nipunkalsotra](https://github.com/nipunkalsotra)**

<br>
<sub><i>If you can't verify it, you can't trust it.</i></sub>

</div>
