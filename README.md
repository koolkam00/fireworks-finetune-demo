# Specialized intelligence, demonstrated

An application project for the **Strategic Projects Lead** role at Fireworks AI — built in one day for about $120.

**Live page:** https://koolkam00.github.io/fireworks-finetune-demo

## What this is

I fine-tuned small open models on Fireworks to extract eight structured fields from executed credit agreements, benchmarked them honestly against a frontier API, and priced the rent-vs-own decision that follows.

| Model (49 held-out docs) | Field accuracy | Cost / 1K docs | Median latency |
| --- | --- | --- | --- |
| GPT-5.6-sol *(rented frontier, reference)* | 97.4% | $52.91 | 6.0s |
| Llama-3.1-8B — base | 66.9% | $1.78 | 3.0s |
| **Llama-3.1-8B — tuned (ours)** | **90.3%** | **$1.77** | **3.4s** |
| Qwen3-8B — tuned *(experiment)* | 83.0% | $1.86 | 5.3s |
| DeepSeek V4-Flash 284B — base | 86.7% | $1.82 | 11.1s |

A ~$2 LoRA fine-tune moved an 8B from 67% to 90% field accuracy at roughly 1/30th the frontier's cost and half its latency.

## Method

- **Benchmark** — 289 executed credit agreements pulled from SEC EDGAR (2019–2026, one per company, amendments filtered out), trimmed to definition-bearing excerpts.
- **Answer key** — frontier-drafted labels; 238 documents became training demonstrations, 50 were locked away as the exam. The exam key was independently audited field-by-field by a second model family (396/400 confirmed), and every contested call was human-adjudicated — three of five rulings went against the frontier's drafts.
- **Tuning** — supervised LoRA (rank 16, 2 epochs) on Fireworks across three model families.
- **Scoring** — one eval harness, same prompt and excerpts for every model: fuzzy name matching, normalized dates and amounts, set-F1 on facility types, null-discipline enforced. Cost and latency recorded per call.

Honest caveat: where the label drafter and the auditor share a blind spot, the frontier column carries some self-agreement bias — read it as a ceiling, not a verdict.

## What's in the page

- The scoreboard above, with per-field accuracy breakdowns
- An interactive **rent-vs-own breakeven calculator** seeded with the measured numbers, not estimates
- A sample explorer showing the models reading real agreements side by side
- Four developer-experience findings from onboarding to Fireworks as a stranger, each with a proposed fix
- The private-markets GTM wedge I'd run

## Repo contents

- `index.html` — the entire site. Self-contained: no build step, no dependencies, no external assets.
- `calculator.html` — the breakeven calculator as a standalone page (it is also embedded in `index.html`).

## Disclaimer

No affiliation with Fireworks AI — this is an independent application project. Pricing reflects public list rates as of August 2026.

Andrew Kam · andrew.kam00@gmail.com
