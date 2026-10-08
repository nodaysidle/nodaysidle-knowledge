---
type: inbox-idea
status: open
topic_slug: prompt-optimizer-multi-provider
created: 2026-10-08
owner: nodaysidle
tags:
  - inbox
  - prompt-optimizer
  - llm-providers
  - feature-backlog
priority: medium
---

# Multi-Provider Engine Switch (DeepSeek + Gemini + OpenAI) for Prompt Optimizer

## Summary

Expand the rewriter backend in `nodaysidle-prompt-optimizer` to support switching between multiple foundation model providers:
1. **DeepSeek Direct API** (`deepseek-chat` / `deepseek-reasoner` / V3 / R1)
2. **Google Gemini API** (`gemini-2.5-flash`, `gemini-2.5-pro`)
3. **OpenAI Direct API** (`gpt-4o`, `gpt-4o-mini`, `o3-mini`)

## Motivation & Architecture

Currently, the optimizer routes prompt rewrites through the DeepSeek Platform API (`https://api.deepseek.com/chat/completions`) and audits with TypeSafe Jev.
Adding multi-provider support provides:
- **Redundancy & Failover:** Zero single-point-of-failure if an API key runs out of quota or an upstream API experiences rate limits.
- **Provider-Specialized Optimization:** Gemini excels at multimodal image/video prompt reasoning; OpenAI excels at strict structured schemas; DeepSeek provides cost-effective high-density reasoning.
- **Client-Side Key Management:** Keep API keys persisted in encrypted/local browser storage (`localStorage`), sending keys via custom request headers (`x-deepseek-key`, `x-gemini-key`, `x-openai-key`).

## Implementation Checklist

- [ ] Provider selector dropdown in Settings Panel (`settings-panel.tsx`) and quick-switch badge in the main workspace header.
- [ ] API Key fields for OpenAI and Gemini in Settings Context (`settings-context.tsx`).
- [ ] Unified server-side provider router in `src/lib/providers/` (`chat.ts`, `deepseek.ts`, `gemini.ts`, `openai.ts`).
- [ ] Preserve TypeSafe Jev diagnostics and Quality Gate regardless of which LLM provider does the rewriting.
- [ ] Fallback/Auto-retry mechanism if primary provider returns 429/5xx.

## Reference Links

- Codebase: `/home/arch/dev/nodaysidle/nodaysidle-prompt-optimizer`
- Concept Note: [[wiki/concepts/nodaysidle-prompt-optimizer-overview]]
- Live App: https://nodaysidle-prompt-optimizer.vercel.app
