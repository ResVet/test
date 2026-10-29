# Hackathon Playbook

Built and checked on 2026-10-29. Everything marked ✅ was tested live in this environment.

## 1. What you have ready

### Accounts and deployment
| Tool | Status | Use it for |
|---|---|---|
| GitHub (`ResVet`) | ✅ connected | Repo, branches, PRs, Actions |
| Netlify (5 existing sites) | ✅ connected | One-command deploys of the demo URL. **Deploy early, deploy often.** |
| Google Drive | ✅ connected | Pulling briefs and datasets, saving the pitch deck |
| Claude Artifacts | ✅ | Hosted pages, dashboards, slide decks with a shareable link |
| Claude Docs | ✅ | Spec and pitch script you can co-edit |
| Figma, Notion, Slack, Linear, Asana, Atlassian, Intercom | ❌ **failed to connect** (proxy 403) | Reconnect in claude.ai → Settings → Connectors **before** the event if you need them |
| Scite | ❌ connection not finished | Finish OAuth in claude.ai connector settings |

### Research (to back your problem statement with real evidence)
alphaXiv (arXiv papers), Consensus, SciSpace, PubMed, bioRxiv/medRxiv, Wiley Scholar Gateway, plus web search. Judges like a statistic with a source on the problem slide.

### Toolchain in the cloud container
Node 22, npm, pnpm, Bun 1.4, Python 3.13, uv, Rust 1.97, Docker, gcloud, gh, Playwright and Chromium (for screenshots and E2E tests). Not installed: Go, Deno.

### Skills: which ones to use when
| Phase | Ask for / invoke |
|---|---|
| Idea → spec | `ecc-core:plan-prd`, `ecc-core:blueprint`, `ecc-extras:product-lens`, `ecc-extras:market-research`, `anthropic-skills:deep-research` |
| Architecture | `ecc-core:plan`, `ecc-core:api-design`, agent `ecc-core:architect` |
| Build fast | `ecc-core:orch-build-mvp`, `ecc-core:feature-dev`, `ecc-core:prp-implement`, `ecc-core:gan-build` |
| AI features | `claude-api` (latest model IDs, tool use, streaming, caching) |
| UI / design | `ui-ux-pro-max:ui-ux-pro-max`, `ecc-core:frontend-design-direction`, `ecc-core:make-interfaces-feel-better`, `ecc-core:motion-patterns`, `dataviz` |
| Quality gate | `code-review`, `security-review`, `code-review-graph:review-changes` (impact analysis), `ecc-core:verification-loop`, `ecc-core:e2e-testing`, `run` |
| Fix broken builds | `ecc-core:build-fix`, `ecc-core:react-build` |
| Demo and pitch | `ui-ux-pro-max:slides`, `anthropic-skills:pptx`, `ecc-extras:frontend-slides`, `ecc-extras:investor-materials`, `marketing-skills:launch`, `marketing-skills:copywriting`, `ecc-extras:ui-demo`, `ecc-extras:remotion-video-creation` |
| Handover between sessions | `handoff:save` / `handoff:pickup`, `ecc-core:save-session` |

## 2. Default stack (pick unless the brief says otherwise)
- **Web app:** Vite + React + TypeScript + Tailwind, deployed to Netlify.
  `pnpm create vite@latest app -- --template react-ts`
- **Full-stack:** Next.js (`pnpm create next-app@latest`) with Netlify Functions or Next route handlers.
- **Python / ML backend:** FastAPI + uv (`uv init api && uv add fastapi uvicorn`).
- **AI:** Claude API through the Anthropic SDK. Keep the key in an env var and **never commit it**.
- **Data:** SQLite or Supabase. Do not set up infrastructure you cannot demo.

## 3. Timeline (scale to the event length; times shown for 24h)
| When | Goal | Exit criterion |
|---|---|---|
| 0:00–0:45 | Read the brief and judging criteria **twice**. Pick one problem and one user. | One-sentence pitch written down |
| 0:45–1:30 | Spec: 3 must-have features, the rest cut. Sketch the demo path first. | `SPEC.md` committed |
| 1:30–2:00 | Scaffold, then deploy "hello world" to Netlify | Live URL works |
| 2:00–14:00 | Build the **demo path** end-to-end, then deepen it | Demo path works on the live URL |
| 14:00–18:00 | Polish UI, empty/error/loading states, seed data | Looks finished on a phone and on the projector |
| 18:00–20:00 | **Feature freeze.** Code review, security review, fix | No known crash on the demo path |
| 20:00–22:00 | Deck, 2-minute pitch, backup demo video | Rehearsed 3 times, under time |
| 22:00–24:00 | Buffer. README, submission form, final deploy | Submitted with **≥30 min to spare** |

## 4. Rules that win hackathons
1. **Optimise for the judging criteria**, not for technical purity. Map every feature to a criterion.
2. **The demo is the product.** Hardcode or seed anything that isn't on the demo path.
3. **Always keep a working deploy.** Commit and push small; never break `main` in the last 4 hours.
4. **Record a backup demo video** in case Wi-Fi or the API fails on stage.
5. **One wow moment**: a live AI response, a real-time update, a striking visualisation.
6. **Secrets stay out of git**: use `.env`, check `git diff` before every push.
7. **Submit early**, then update. Late uploads fail.

## 5. Pitch template (2–3 minutes)
1. **Hook (15s):** a real person and their pain, with one sourced number.
2. **Problem (20s):** why existing solutions fail.
3. **Solution (15s):** one sentence.
4. **Live demo (60–90s):** the happy path, one wow moment.
5. **How it works (20s):** architecture in one diagram; mention the AI/tech used.
6. **Impact and next steps (15s):** who uses it, what it scales to.
7. **Team / ask (10s).**

## 6. Submission checklist
- [ ] Live URL works in an incognito window and on a phone
- [ ] README: problem, solution, screenshots, how to run, tech stack, team
- [ ] Repo is public (if required) and has no secrets (`git log -p | grep -iE "api[_-]?key|secret|token"`)
- [ ] Demo video uploaded (≤ length limit)
- [ ] Deck exported to PDF
- [ ] All required form fields, team members, and the track/category selected

## 7. How to work with Claude at the event
Paste the brief and the judging criteria in your first message, plus the event length and team size. Then say "spec it", "scaffold and deploy", "build feature X", "review and harden", "make the deck". Each one maps to the skills above.
