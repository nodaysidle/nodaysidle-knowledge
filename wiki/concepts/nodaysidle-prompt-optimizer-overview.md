---
type: wiki-note
note_kind: concept
topic_slug: prompt-optimizer
status: active
created: 2026-10-07
updated: 2026-10-07
tags:
  - wiki
  - prompt-optimizer
  - ai-tools
  - deepseek
  - typesafe-jev
---

# NODAYSIDLE Prompt Optimizer — overview

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

## TypeSafe Jev System One Integration

- **Preflight Diagnostics (~80ms):**
  - Evaluates inputs using Jev primitives: `score` (0..3 clarity), `noul` (ambiguity, lack of negative constraints, lack of persona/role, injection/jailbreak risk), and `choice` (suggested category).
  - For video prompts: runs dedicated questions for temporal motion dynamics (`lacks_temporal_action`) and cinematographic camera path (`lacks_camera_movement`).
  - Diagnostic flaws are injected directly into DeepSeek rewrite instructions, making rewrites targeted rather than generic.
- **Quality Gate:**
  - Post-generation Jev evaluation verifying core intent preservation (`intent_preserved >= 0.7`) and guarding against cognitive bloat/over-engineering (`over_engineered <= 0.6`).
- **Interactive UI:**
  - Live health audit score (0-100), health gauge, and dimension tiles (switching to "Camera & Motion" when auditing video prompts).
  - Side-by-side view, word-level diff viewer (`diff` tokenization), and live testing playground.

## Verification & Deployment

- **Repository:** `https://github.com/nodaysidle/nodaysidle-prompt-optimizer` (branch `master`)
- **Local Clone:** `/home/arch/dev/nodaysidle/nodaysidle-prompt-optimizer`
- **Production Host:** Vercel (`https://nodaysidle-prompt-optimizer.vercel.app`)
- **Licence:** MIT
