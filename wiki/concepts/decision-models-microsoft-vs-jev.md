---
type: wiki-note
note_kind: concept
topic_slug: decision-models-microsoft-vs-jev
status: active
created: 2026-10-10
updated: 2026-10-14
tags:
  - wiki
  - decision-models
  - typesafe-jev
  - microsoft-decision-1
  - openrouter
  - ai-architecture
---

# Decision Models: Microsoft-Decision-1 vs TypeSafe Jev

## Prompt Optimizer correction (2026-10-14)

- [vault] The Prompt Optimizer rows/diagram below describe its older 2026-10-10 automatic-provider architecture. Current production defaults to **app-server heuristics**; OpenRouter and TypeSafe are explicit diagnostic choices, with consented heuristic fallback and no silent cross-provider cascade. No fixed sub-100ms latency is claimed or newly benchmarked by this implementation.
- [vault] See [[wiki/concepts/nodaysidle-prompt-optimizer-overview]] and [[artifacts/prompt-optimizer/audit-fixes-and-deploy-2026-10-14]]. This correction applies to Prompt Optimizer only; no new verification of the other projects or historical comparison metrics was performed. Historical content is retained below.

## Summary

In October 2026, Microsoft introduced **Microsoft-Decision-1** (Office of the CTO / Achint Srivastava), entering the fast, structured "decision model / System One" category established by **TypeSafe Jev**. Both models reject free-form conversational text generation in favor of fast, typed probabilistic judgments (`choice`, `score`, `noul`) over structured state.

This note documents their benchmark differences, calibration characteristics, API signatures, and the strategic hybrid architecture adopted across the **NODAYSIDLE** workspace.

---

## 1. Technical & Benchmark Comparison

Both models were benchmarked across 36 blinded datasets spanning nearly 150,000 questions (including the public *JevBench* leaderboard):

| Metric / Dimension | TypeSafe Jev (v1.13.0) | Microsoft-Decision-1 | Practical Assessment |
| :--- | :--- | :--- | :--- |
| **Foundation & Architecture** | Purpose-built System One engine | Post-trained **Qwen3.5-9B** (planned MAI / OpenAI rebases) | Decision-1 leverages open weights scale; Jev is specialized proprietary. |
| **Median Latency (P50)** | **240 ms** | **85 ms** (125 ms P95) | ⚡ **Microsoft-Decision-1 is ~2.8× faster.** Critical for hot-path agent loops. |
| **Accuracy (36 Benchmarks)** | **82.3%** | **83.5%** | 🎯 **Microsoft-Decision-1** has a slight +1.2% advantage across broad generalization sets. |
| **Probability Calibration** | **93.7** (#1 ranked) | **92.2** (#3 ranked) | ⚖️ **TypeSafe Jev is superior in calibration.** 100 represents perfect empirical alignment between confidence $P$ and actual accuracy. |
| **Robustness / Perturbation Flips** | Stable | **1.3%** flip rate under 8 perturbation types; 0% flips on option reordering/paraphrasing | Both exhibit strong immunity to harmless formatting noise. |
| **API Endpoints** | `api.typesafe.ai/v1/system_one` | Azure AI Foundry & OpenRouter (`/api/alpha/decisions`) | OpenRouter gives seamless universal access without dedicated enterprise Azure setups. |
| **Pricing** | **$0.042 / 1M input tokens** | **$0.042 / 1M input tokens** | 🤝 **Exact price parity.** Output tokens are free on both engines. |

---

## 2. API Contract & Primitives

Microsoft-Decision-1 directly adopts the schema paradigms popularized by Jev on OpenRouter's `/api/alpha/decisions` endpoint:

* **State:** Arbitrary JSON object containing the context payload.
* **Primitives:**
  1. `noul` (Boolean / Yes-No): Returns calibrated probability $P(\text{yes}) \in [0, 1]$.
  2. `score` (Ordinal Rubric): Takes ordered `criteria` (2–10 levels), returns weighted `score` ($0 \dots n-1$), `probabilities`, and `confidence`.
  3. `choice` (Categorical): Takes a map of options, returns `choice`, per-option `probabilities`, and `confidence`.

```json
POST https://openrouter.ai/api/alpha/decisions
{
  "model": "microsoft/microsoft-decision-1",
  "state": { "prompt": "..." },
  "questions": {
    "clarity": {
      "type": "score",
      "instructions": "How clear is `prompt`?",
      "criteria": ["Vague", "Basic", "Clear", "Exemplary"]
    },
    "is_ambiguous": {
      "type": "noul",
      "instructions": "Is the scope of `prompt` ambiguous?"
    }
  }
}
```

---

## 3. Workspace Architecture Strategy

Rather than treating them as mutually exclusive competitors, the NODAYSIDLE workspace uses a **hybrid split** based on their core technical strengths:

```mermaid
flowchart TD
    Task["Incoming Judgment Task"] --> LatencyCheck{"Is task in a hot user loop or public web traffic?"}
    
    LatencyCheck -->|Yes (<100ms budget)| MS["Microsoft-Decision-1 (OpenRouter)"]
    LatencyCheck -->|No (Calibration > Latency)| TS["TypeSafe Jev"]
    
    MS --> KurekScreen["Kurek: Screen Context Detection (~85ms)"]
    MS --> OptimizerWeb["Prompt Optimizer: Real-time UI Linting (~85ms)"]
    MS --> AgentRouting["Agent Loops & Model Routing"]
    
    TS --> KurekMem["Kurek: Muse Memory Triage & Boundary Hoisting"]
    TS --> Cascade["Cascade V3: Architecture Blueprint Gating"]
    TS --> JevReview["jev-review: Security & Correctness Risk Matrices"]
```

### 1. Hot Real-Time Paths → Microsoft-Decision-1
* **Kureksistant (`kurekizmo`):**
  * Evaluates `needs_screen` before voice response generation.
  * Dropping from 240ms to 85ms saves ~155ms of voice latency on middle-click hardware triggers.
  * *(ATLAS 2026-10-15 13:38 UTC: **these latency figures are unqualified — do not quote them.** The 240 ms and 85 ms values are the two models' **quoted P50 figures**, not a Kurek measurement: no bench script, CI run or artifact backs them, and "~155 ms saved" is that note's own assertion (see `_audit/log.md` 2026-10-10, lines 504 and 509, the latter reading "live verified in daemon venv"). The **~85 ms** labels in the diagram above and the Prompt Optimizer "sub-100ms" line below carry the same caveat. Same class as the "~0.8ms trigger" and "<0.1s" caveats in [[wiki/concepts/kureksistant-overview]] lines 54 and 56.)*
* **Prompt Optimizer (`nodaysidle-prompt-optimizer`):**
  * Real-time debounced typing audit across 5 dimensions (`clarity`, `is_ambiguous`, `lacks_constraints`, `lacks_role`, `injection_risk`).
  * Sub-100ms speed eliminates typing lag; OpenRouter handles public Vercel concurrency without single-key thread limits.

### 2. High-Stakes Gating & Auditing → TypeSafe Jev
* **Kureksistant Memory & Alignment:**
  * Background triage into `MEMORY.md` and hoisting hard safety boundaries into `~/ALIGNMENT_SYNTHESIS.md`.
  * Gated strictly on calibrated thresholds ($P > 0.85$); Jev’s 93.7 calibration prevents false boundary alarms.
* **Cascade V3 (`nodaysidle-cascade-v3`):**
  * Blueprint acceptance verifiability and foreign-stack leakage gating.
* **Code Auditing ([`jev-review`](file:///home/arch/.agents/skills/jev-review/SKILL.md)):**
  * Global CLI tool scanning code diffs across 5 dimensions (`correctness`, `security`, `reliability`, `compatibility`, `test_coverage`).
