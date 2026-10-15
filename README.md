# Prompt Granularity and Functional Outcomes in AI Coding Agents

This repository holds the materials for an exploratory study of how developers group instructions for AI coding agents. The same ten implementation work units were given to three commercial agent configurations under four schedules, with three repetitions each (36 builds).

The accompanying manuscript is prepared for **IEEE Intelligent Systems**:

> N. Kumar and R. Guliani, "Prompt Granularity and Functional Outcomes in AI Coding Agents," manuscript prepared for *IEEE Intelligent Systems*, 2026.

The manuscript files sit next to this repository, not inside it.

## What was compared

Each build started from the same Vite, React, and TypeScript starter and used DummyJSON. The ten work units cover login and session handling, the authenticated shell, catalog loading, product cards and images, search, reviews, comments, cart integration, the cart screen, and order confirmation.

The wording inside each work unit is the same across schedules, including the requirement that a signed-in user stay on the Products or Cart page after refresh. The schedules differ in message grouping and in the instructions that tell the agent when to stop or continue.

| Schedule | Messages | Work units in successive messages |
|---|---|---|
| P1 | 1 | 1-10 |
| P3 | 3 | 1-2; 3-7; 8-10 |
| P6 | 6 | 1; 2-3; 4-5; 6-7; 8; 9-10 |
| P10 | 10 | One unit per message |

The three configurations are Cursor Grok 4.6 High Fast, Claude Sonnet 5 High, and GPT-5.6 Sol Medium. They are complete commercial setups, with different effort settings and tools. They are not a comparison of base models under identical tooling.

## Headline results

Geometric mean recorded token use rose from 1.30 million (P1) to 2.34 million (P3), 5.06 million (P6), and 6.42 million (P10). All 18 builds on the three-prompt and six-prompt schedules scored 25/25 on the functional checklist. Across all builds the recorded total is 877 of 900 checklist classifications. That total includes inferred and blocked outcomes, so it is not 900 independent test executions.

These figures describe the tested schedules. They do not isolate prompt count from phase boundaries, and they do not identify a universal prompt count.

## Repository layout

```
.
├── result.xlsx          # Recorded tokens, scores, notes, and Lighthouse cells
├── base-setup/          # Shared Vite + React + TypeScript starter and spec/
├── prompts/             # The 20 implementation prompts (P1, P3, P6, P10)
├── reports/             # Lighthouse screenshots that were captured
└── research-code/       # One application snapshot per build
    ├── claude sonnet 5 high/
    ├── cursor grok 4.6 high fast/
    └── gpt 5.6 sol medium/
        └── r1/ r2/ r3/
            └── P1/ P3/ P6/ P10/
                └── starter/
```

- `result.xlsx` is the analysis source. It has an environment sheet, a checklist sheet, and one sheet per configuration.
- `prompts/` contains one file for P1, three for P3, six for P6, and ten for P10. There is no separate validation-prompt file. Each schedule ends with a production build and type check.
- `research-code/<configuration>/rN/P#/starter/` is the application produced by that build.
- `reports/` stores login, product, and cart screenshots when the audit stayed on the intended page. Missing images match page audits that could not be completed.

## How to read a build

Open `research-code/<configuration>/rN/<schedule>/starter/`, install dependencies with `npm ci`, and run `npm run dev`. The starter listens on port 8080. The public DummyJSON demonstration account used in the checklist is `emilys` / `emilyspass`.
