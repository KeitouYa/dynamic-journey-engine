# Dynamic Journey Engine

A small rule engine for patient care journeys, written in TypeScript.

A patient's journey (for example an IVF cycle) is a set of steps with prerequisites. Lab results, insurance decisions, signed consents and staff actions keep arriving, and each one can change what the patient is allowed to do next. This engine takes that new information, re-evaluates the journey with versioned rules, and decides which steps are ready, blocked, waiting on missing data, or need a clinician to look at them. Every decision is recorded with the rule and data behind it.

The engine is deterministic. Rules are written by people and stored as data. AI may help extract facts from documents, but those facts don't count until a person confirms them.

## Goals

- Rules live in config, not in code, and every published rule set has a version
- Missing or stale data is treated as unknown, never as a failed check
- Steps depend on each other, and a blocked step blocks everything after it
- Every change is stored with the rule version, the data it used, and a readable explanation
- The same event processed twice has no extra effect
- Unclear cases go to a person instead of moving forward automatically

## Status

Early work in progress. It's being built in small steps, each one tested before the next.

| Step | What it adds |
|---|---|
| 0 | Project setup, test runner, CI on every push |
| 1 | A single rule and its evaluation (satisfied, not satisfied, unknown) |
| 2 | Several rules per step with clear precedence, plus step dependencies |
| 3 | Evidence handling for stale data and unconfirmed AI extractions |
| 4 | Postgres storage with state, decisions and explanations in one transaction |
| 5 | Event handling with re-evaluation per patient and duplicate protection |
| 6 | Rule set versions that running journeys stay pinned to |

## Tech

TypeScript, Node.js, PostgreSQL, Vitest, GitHub Actions.

## Running it

Setup instructions will be added with step 0.
