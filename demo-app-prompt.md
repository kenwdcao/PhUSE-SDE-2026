# Prompt: Build the PhUSE SDE 2026 demo — ADaM Agent (Ink + AI SDK)

You are an AI coding agent. Build a minimal but working terminal application in TypeScript that will be used to capture **screenshots and short GIFs** for a 30-minute conference talk at PhUSE SDE 2026. The app will most likely not be run live; it needs to look good in static captures and short recordings, and the four tool calls must produce visibly distinct, screenshot-worthy outputs.

The talk's goal is to show how **Ink** (React in the terminal) and the **Vercel AI SDK** combine to produce an internal clinical-programming tool. Keep the code compact and readable — every file may end up visible in a slide.

---

## Stack

- **Runtime:** Node.js ≥ 20 (or Bun, speaker's choice — default Node)
- **Language:** TypeScript, strict mode
- **UI:** [Ink](https://github.com/vadimdemedes/ink) v5+
- **AI:** [`ai`](https://www.npmjs.com/package/ai) (Vercel AI SDK v5+) with a provider of choice (default: `@ai-sdk/anthropic`, model `claude-sonnet-4-6`)
- **Validation:** `zod` for tool input/output schemas
- **Spec parsing:** `xlsx` (SheetJS) for Pinnacle 21 spec files

Do **not** add state management libraries, testing frameworks, or build tooling beyond `tsx` / `tsc`. This is a demo, not a product.

---

## Project layout

```
adam-agent/
├── package.json
├── tsconfig.json
├── src/
│   ├── index.tsx           # Ink app entry, top-level <App />
│   ├── agent.ts            # AI SDK streamText() call, tool registration
│   ├── tools/
│   │   ├── read-spec.ts
│   │   ├── read-skill.ts
│   │   ├── adam-plan.ts
│   │   └── gen-program.ts
│   ├── ui/
│   │   ├── SpecPanel.tsx   # Renders structured spec from read_spec
│   │   ├── PlanStream.tsx  # Renders streamed markdown plan
│   │   ├── ApprovalPrompt.tsx
│   │   └── StatusLine.tsx
│   └── types.ts            # Shared TS types (DatasetSpec, Skill, etc.)
├── specs/
│   ├── adsl.xlsx           # Sample P21-format ADSL spec
│   └── adlb.xlsx           # Sample P21-format BDS spec
└── skills/
    ├── adsl.md
    ├── bds.md
    ├── occds.md
    └── other.md
```
