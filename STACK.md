# Stack Assumptions

The Carmack Council skills are opinionated for the stack below. If you use a different stack, fork and adapt. This file lists every stack-specific assumption, where it appears, and what to change.

## The Stack

| Layer | Technology | Alternative examples |
|-------|-----------|---------------------|
| Language | Python 3.11+ (type hints, async/await) | — |
| HTTP framework | FastAPI | Flask, Starlette, Litestar |
| Bot framework | python-telegram-bot | aiogram, Telethon |
| Validation | Pydantic v2 | attrs, msgspec |
| ORM | SQLAlchemy async | Tortoise ORM, raw SQL |
| Database | SQLite / Firestore | Postgres, MongoDB |
| Auth | Custom (Telegram user ID based) | — |
| UI layer | Telegram inline keyboards / conversation UX | — |
| Deployment | Docker, Google Cloud Run, Railway | Fly.io, AWS |
| AI layer | Gemini via LiteLLM (http://89.167.90.181:4000) | direct API calls |
| Testing | pytest, pytest-asyncio, httpx | unittest |

---

## Where Assumptions Live

### SKILL.md files — Stack Context sections

Every SKILL.md has a "Stack Context" section near the top. This is the primary place to update.

| File | What to change |
|------|---------------|
| `skills/council-review/SKILL.md` | Stack Context section. Update framework, API layer, ORM, DB, auth, UI, deployment target. |
| `skills/council-plan/SKILL.md` | Stack Context section. Same stack list. |
| `skills/council-implement/SKILL.md` | Stack Context section. Same stack list. |
| `skills/spec-writer/SKILL.md` | No stack context section — spec-writer is stack-agnostic by design. |

### SKILL.md files — Subagent prompts

The council-review and council-plan SKILL.md files contain subagent prompt templates that reference specific technologies.

| Pattern | Where it appears | What to change |
|---------|-----------------|---------------|
| "FastAPI routers" | council-review subagent prompts (Backend, Telegram UX), council-plan subagent prompts | Replace with your API layer |
| "SQLAlchemy" / "SQLite" / "Firestore" | council-review subagent prompts (Leach, Backend), council-plan subagent prompts | Replace with your ORM/DB |
| "Telegram inline keyboards" | council-review subagent prompts (Telegram UX Expert), council-plan subagent prompts | Replace with your UI approach |
| "Telegram user ID based" auth | council-review and council-plan Stack Context | Replace with your auth provider |
| "Docker" / "Cloud Run" | council-review Stack Context, council-plan Docker/Deploy subagent | Replace with your deployment target |
| `skills/ui-architect/SKILL.md` | council-review Saarinen subagent, council-plan Saarinen subagent | Optional read — remove if you don't have this skill |
| `skills/ux-architect/SKILL.md` | council-review Friedman subagent, council-plan Friedman subagent | Optional read — remove if you don't have this skill |
| `skills/test-architect/SKILL.md` | council-review Beck subagent | Optional read — remove if you don't have this skill |

### Reference documents

The reference docs contain stack-specific patterns and examples throughout. These are the most work to adapt.

| Reference | Stack assumptions | What to change |
|-----------|-----------------|---------------|
| `references/security.md` | Telegram user ID auth, FastAPI middleware, SQLAlchemy queries | Replace with your auth/API/ORM security patterns |
| `references/quality-backend.md` | FastAPI endpoints, Pydantic models, python-telegram-bot handlers, asyncio patterns | Replace with your API layer, ORM, and deployment patterns |
| `references/quality-frontend.md` | N/A — no frontend framework. UI is Telegram inline keyboards and conversation UX | Adjust for your UI approach |
| `references/quality-postgres.md` | SQLAlchemy async, SQLite/Firestore | Replace with your ORM and DB provider. Core DB principles are universal |
| `references/quality-testing.md` | pytest, pytest-asyncio, httpx for FastAPI test client | Replace with your test framework and tooling |
| `references/quality-llm.md` | General LLM pipeline principles — largely stack-agnostic. Gemini via LiteLLM | — |
| `references/quality-ui.md` | Telegram bot UX — inline keyboards, conversation flows, message formatting | Replace with your UI approach |
| `references/quality-ux.md` | Bot conversation UX patterns | Adjust for your product type and user context |
| `references/refactoring.md` | FastAPI, SQLAlchemy, python-telegram-bot patterns | Replace with your stack's refactoring patterns. Core refactoring principles are universal |

### Spec-writer references

The spec-writer references (`references/spec-writer/`) are stack-agnostic. No changes needed for a different stack.

---

## How to Fork

1. **Edit this file** — Update "The Stack" table with your technologies.
2. **Update Stack Context sections** — In each SKILL.md, replace the Stack Context block.
3. **Update subagent prompts** — Search for the patterns listed above and replace.
4. **Update reference docs** — This is the heavy lift. Each reference doc has stack-specific examples woven throughout. Replace them with equivalent patterns from your stack. The principles themselves (e.g., "crash on programmer errors, handle operational errors") are universal — only the examples change.
5. **Rebuild** — Run `./scripts/build.sh` to produce updated `.skill` packages.

Start with the SKILL.md files (fast, high impact), then work through the reference docs one at a time.
