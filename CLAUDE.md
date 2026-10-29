# Project rules (hackathon mode)

- Read `HACKATHON.md` first. Judging criteria and the demo path come before everything else.
- Keep the live deploy working. Small commits, push often, never leave `main` broken.
- Default stack: Vite + React + TypeScript + Tailwind on Netlify; FastAPI + uv for Python backends; Claude API for AI features (look up current model IDs with the `claude-api` skill).
- Secrets live in `.env` (gitignored) or in Netlify environment variables, never in code.
- Before calling something done, run it: build, run the app or tests, and check the demo path in a browser (Playwright is preinstalled).
- Scope ruthlessly: hardcode or seed anything that isn't on the demo path.
