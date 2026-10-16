---
type: wiki-note
note_kind: concept
topic_slug: prompt-optimizer
status: active
created: 2026-10-07
updated: 2026-10-14
tags:
  - wiki
  - prompt-optimizer
  - ai-tools
  - deepseek
  - typesafe-jev
---

# NODAYSIDLE Prompt Optimizer overview

## Current deployed state (2026-10-14)

- [vault] A preservation-first, desktop-first workbench for user/system/image/video prompt text. Default **minimal** editing, optional **structured** and **creative** modes; no invented missing-context placeholders. Draft/candidate editing, frozen-original diff, actionable diagnostic questions, Undo, versioned history and paired **text** evaluation.
- [vault] DeepSeek models: `deepseek-flash` and `deepseek-v4-pro`, with thinking explicitly disabled. Default diagnosis uses **app-server heuristics**, not browser-only processing; it sends no prompt to an AI provider. OpenRouter/TypeSafe diagnosis is explicitly selected; fallback requires consent and stays rule-based, not a silent external-provider cascade.
- [vault] Honest quality states (`passed`, `needsReview`, `unavailable`), strict model/API schemas, cancellation/stale-result protection, deadlines/output limits and single ratio/lens replacement. Short clear prompts and static-camera intent are valid. No guaranteed production-ready, exact-identity or fixed-latency claims.
- [vault] BYOK/session-memory access with optional plaintext remembering. Legacy browser credentials remain untouched until explicit Forget; Settings can import valid keys for this session. Every server-key fallback requires a private `APP_ACCESS_TOKEN`; current production had no configured server variables at deployment check. Per-instance throttle is not a durable quota.
- [vault] Image/video profiles are versioned prompting guidance with capability/source limits, **not rendering integrations**. FLUX.2 has no negative field. Actual visual generation and multi-provider rewriting are not implemented. Paid-model/renderer quality was not benchmarked.
- [vault] Editor-first dark UI, accessible dialogs/keyboard history, measured text contrast and owner-supplied silver N mark. **90 unit tests and 5 browser tests** passed locally with lint/typecheck/build and a clean production dependency audit; provider flows use mocks. GitHub CI was not run in this session.
- [vault] **Production:** https://nodaysidle-prompt-optimizer.vercel.app/; latest code `03aac47`, deployment `dpl_EP2DWUpWzXnN3AifwtkjVKtCkdNW`, READY and live-logo verified.
- [vault] **Source continuity warning:** original clone `master` is still `818eed1`. New code lives in `/home/arch/.local/share/opencode/worktree/6f72e1/optimizer-audit-fixes`, retained by local branch `audit/nodaysidle-logo`, **not merged/pushed**. Redeploying original `master` would replace these changes.

Full changes, evidence and limitations: [[artifacts/prompt-optimizer/audit-fixes-and-deploy-2026-10-14]]. Resume: [[sessions/2026-10-14-prompt-optimizer-session]].

## Historical snapshot (2026-10-07 to 2026-10-10, superseded)

The original overview below is retained for history. Old model names, placeholder insertion, forced video timing, automatic provider fallback, latency/quality claims and the older deployment describe previous behavior, **not the current production app**.

## Summary

`nodaysidle-prompt-optimizer` is a production-grade prompt engineering workbench built with Next.js 16 (App Router, Turbopack), React 19, and Tailwind CSS v4. It couples **DeepSeek Platform Flash API** (`deepseek-chat` / `deepseek-reasoner`) with **TypeSafe Jev System One** probabilistic rubric diagnostics to audit, condition, rewrite, and quality-gate prompts with sub-100ms feedback and zero CORS exposure.

## Core Capabilities & Modalities

The optimizer supports four distinct prompt paradigms (`user`, `system`, `image`, and `video`):

1. **User Prompts (`user`):**
   - Targets general LLM queries (ChatGPT, Claude, Cursor).
   - Improves instruction clarity, reasoning triggers, structural boundaries, missing context placeholders (`[brackets]`), and negative criteria.

2. **System Prompts (`system`):**
   - Targets governing personas and autonomous agents.
   - Enforces strict operational boundaries, persona consistency, output schema contracts (JSON/Markdown), and anti-hallucination guardrails.

3. **Image Prompts (`image`):**
   - Targets diffusion and multimodal models: Google Nano Banana (Gemini image), GPT-1.5 Image, Midjourney v6, and Flux.1.
   - Enriches lighting, camera/lens optics, composition, medium/style, color palette, and aspect ratio without wrapping prompts in raw JSON dictionaries (eliminating copy-paste friction).

4. **Video Generation Prompts (`video`):**
   - Dedicated prompt architecture for foundation video generators: **Google Veo 3.1**, **Google Omni**, **Kling (1.5/2.0)**, and **Runway (Gen-3 Alpha)**.
   - **Output Format Convention:** Clean, section-tagged plain text designed for direct paste into video generation inputs:
     - `[SCENE & SUBJECT]`: Subject appearance, attire/materials, starting pose, and environmental architecture.
     - `[TEMPORAL ACTION & DYNAMICS]`: Second-by-second action progression (e.g. 0-2s start, 2-5s climax, 5-8s resolution), speed changes, contact physics, and secondary effects (tire smoke, dust particles, water spray, cloth/hair simulation).
     - `[CAMERA PATH & CINEMATOGRAPHY]`: Camera trajectories (low-angle tracking, orbital pan, crane push-in, FPV chase), focal length, shutter/motion blur, framing, and depth of field.
     - `[LIGHTING & ATMOSPHERE]`: Dynamic light progression, reflections, volumetric lighting, and color grading.
     - `[NEGATIVE / ARTIFACT GUARDS]`: Excludes static pauses, unnatural morphing, jitter, rubbery limbs, and sudden camera snapping.

## Decision Intelligence Engines (Microsoft-Decision-1 + TypeSafe Jev)

- **Dual-Engine Architecture (Updated 2026-10-10):**
  - **Primary Engine — Microsoft-Decision-1 (OpenRouter `/api/alpha/decisions`):**
    - Post-trained Qwen3.5-9B model delivering **~85ms median latency** on structured decision tasks.
    - Resolves public web concurrency bottlenecks and account thread limits on Vercel.
    - Evaluates 8 questions in a single parallel snap call: `clarity` (0..3 score rubric), `is_ambiguous` (noul), `lacks_constraints` (noul), `lacks_role` (noul), `injection_risk` (noul), `suggested_kind` (choice), plus video-specific `lacks_temporal_action` and `lacks_camera_movement`.
  - **Fallback Engine — TypeSafe Jev:**
    - High-calibration System One model (`jev-1.13.0`, 93.7 calibration score) engaged if OpenRouter key is absent.
  - **Zero-Cost Fallback — Deterministic Heuristics:**
    - Built-in regex and lexical tokenizer engaged if no cloud keys are provided.
- **Quality Gate:**
  - Post-generation evaluation verifying core intent preservation (`intent_preserved >= 0.7`) and guarding against bloat (`over_engineered <= 0.6`).
- **Interactive UI & Client Settings:**
  - Live health audit score (0-100), health gauge, and dimension tiles.
  - Dedicated **OpenRouter** and **TypeSafe** settings cards with local browser key storage (`localStorage`).
  - Side-by-side view, word-level diff viewer (`diff` tokenization), and live playground.

## Verification & Deployment

- **Repository:** `https://github.com/nodaysidle/nodaysidle-prompt-optimizer` (branch `master`)
- **Local Clone:** `/home/arch/dev/nodaysidle/nodaysidle-prompt-optimizer`
- **Production Host:** Vercel (`https://nodaysidle-prompt-optimizer.vercel.app`)
- **Latest Production Release (2026-10-10):** Commit `818eed1` deployed via Vercel CLI (`Ready in 33s`), live verified on `/api/diagnose` with `x-openrouter-key`.
- **Licence:** MIT
- **Comparative Note:** [[wiki/concepts/decision-models-microsoft-vs-jev]]

## Backlog & Future Enhancements

- [[inbox/2026-10-08-prompt-optimizer-multi-provider-engine]] — Multi-provider rewriter backend (DeepSeek, Gemini, OpenAI).

<!-- atlas-2133 -->
## README snapshot: source of truth (2026-10-16 21:33)
- Snapshot: [[wiki/sources/nodaysidle-prompt-optimizer-README]] (public `nodaysidle/nodaysidle-prompt-optimizer` @ `7eacdfb`, committed 2026-10-15T05:19:32+02:00). Owner source of truth (Alan 21:32/21:33). Read it first; it wins over older text on this page.
- Local checkout on arch (read-only `git status` at 21:35, no fetch, so the unpushed count may be stale): `nodaysidle-prompt-optimizer` (master): clean, **1 unpushed commit**.
- Local vs GitHub README diff: README matches GitHub; local master is 1 commit ahead (`d57a093`, unpushed) (SHIP 21:34)

<!-- atlas-2303 -->
- **README demo GIF:** no (SHIP 23:00, [[wiki/sources/catalog-audit-2026-10-16]]).
