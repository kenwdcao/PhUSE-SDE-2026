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
---

## Pinnacle 21 spec format

The spec is a standard P21 define-style `.xlsx` with at least these sheets:

- **`Datasets`** — one row per dataset. Required columns: `Dataset`, `Description` (label), `Class` (e.g. `ADSL`, `BDS`, `OCCDS`, `OTHER`), `Structure`, `Key Variables`.
- **`Variables`** — one row per variable per dataset. Required columns: `Dataset`, `Variable`, `Label`, `Type`, `Length`, `Origin`, `Derivation` (optional, may be blank), `Codelist` (optional).
- **`ValueLevel`** (BDS only, optional) — one row per `PARAMCD` × variable. Required columns: `Dataset`, `Variable`, `Where` (e.g. `PARAMCD = "HGB"`), `Derivation`.

Assume the sample specs in `specs/` conform to this layout. Build `read_spec` defensively enough that missing optional columns do not crash the tool, but do not try to handle arbitrary P21 dialects — this is a demo.

---

## The four tools

All four tools MUST be registered via the AI SDK `tool()` helper with `zod` schemas. Inputs and outputs are strictly typed.

### 1. `read_spec` — read-only, no approval

```ts
input:  { path: string }
output: {
  dataset: string              // e.g. "ADSL"
  label: string
  class: "ADSL" | "BDS" | "OCCDS" | "OTHER"
  structure: string
  keyVariables: string[]
  variables: Array<{
    name: string
    label: string
    type: string
    length?: number
    origin?: string
    derivation?: string
    codelist?: string
  }>
  // BDS-only: per-parameter derivation
  parameters?: Array<{
    paramcd: string
    variableDerivations: Array<{ variable: string; derivation: string }>
  }>
}
```

Reads the P21 xlsx, classifies the dataset, and returns a structured view. For BDS datasets, pivots the `ValueLevel` sheet into `parameters[]`.

### 2. `read_skill` — read-only, no approval

```ts
input:  { datasetType: "ADSL" | "BDS" | "OCCDS" | "OTHER" }
output: { content: string; path: string }
```

Reads `skills/<datasetType>.md` from disk and returns its contents verbatim. Throws if the file does not exist.

### 3. `adam_plan` — text-only, no approval, MUST stream

```ts
input:  { spec: DatasetSpec; skill: string }
output: streamed markdown text
```

Calls the model a second time (nested AI call inside the tool) with a prompt that asks for a **step-by-step implementation plan in markdown, no code**. The plan must stream to the UI as it generates — this is the "streaming" teaching beat, so the tokens must be visibly progressive in a GIF capture.

### 4. `gen_program` — writes to disk, **requires approval**

```ts
input:  { plan: string; skill: string; datasetType: string; outputPath: string }
output: { path: string; lineCount: number }
side effect: writes a .sas file to `outputPath`
```

Before writing, the UI MUST show an approval prompt with the full output path and the number of lines about to be written. Approval is done via the AI SDK's `toolApproval` / `needsApproval` pattern (or equivalent) — do not hand-roll a separate confirmation channel.

On rejection: the tool returns a structured "rejected by user" result and the agent must handle it gracefully (acknowledge in the UI, do not retry the same call).

---

## Ink UI requirements

The UI has to look good in a static screenshot. That means:

- A persistent top bar with the app name and current dataset (`<StatusLine />`)
- A main panel that swaps between states: idle → spec parsed → plan streaming → approval prompt → program written
- The streamed plan renders **with visible line-by-line arrival** (not after buffering)
- The approval prompt is a distinct, framed panel with `[Y]es / [N]o` hints
- Use `ink-spinner` for any waiting states
- Use color sparingly: one accent color (cyan or green), red only for the rejection state
- All text wraps cleanly at 100 columns

---

## Agent loop

Use the AI SDK's `streamText` (or `generateText` with tool loop enabled) to drive the agent. The system prompt:

> You are an ADaM programming assistant. When given a spec path, your job is to:
> 1. Call `read_spec` to understand the dataset.
> 2. Call `read_skill` for that dataset's class.
> 3. Call `adam_plan` to produce a step-by-step plan.
> 4. Call `gen_program` to write a draft SAS program.
> Always call the tools in order. Do not write code yourself.

The user message for the demo run: *"Generate an ADSL program from `specs/adsl.xlsx` and write it to `output/adsl.sas`."*

---

## Sample skill files

Each `skills/*.md` is 10–30 lines of real SAS best-practice guidance for that dataset class. Examples of what `adsl.md` should include: USUBJID/STUDYID key var conventions, treatment variable naming (TRT01P/TRT01A), baseline flag derivation patterns, date imputation rules. `bds.md` should cover PARAM/PARAMCD/PARAMN, AVAL/AVALC, ABLFL, CHG/PCHG patterns.

These files are intentionally readable — the speaker may `cat` one in a screenshot to show "the agent reads this file before writing code."

---

## Sample specs

Generate `specs/adsl.xlsx` and `specs/adlb.xlsx` programmatically (a small Node script is fine) so they're reproducible. Keep them small: ADSL with ~20 variables, ADLB with ~15 variables and 3 parameters (e.g. HGB, WBC, PLT). Real-looking column metadata but no PHI.

---

## Non-goals

- No tests, no CI, no Docker.
- No authentication, no config UI, no dotfiles beyond `.env` for the API key.
- Do not try to actually execute the generated SAS code.
- Do not support spec formats other than the P21 layout described above.
- Do not add a web UI — this is terminal-only. (The talk title mentions web apps, but only to motivate the AI SDK's framework-agnostic design; the demo itself is Ink.)

---

## Deliverables

1. Working `adam-agent/` directory matching the layout above.
2. A `README.md` with: setup (`npm install`, `.env` with `ANTHROPIC_API_KEY`), run command (`npm run dev`), and one paragraph on what the agent does.
3. One sample successful run captured as either four screenshots (one per UI state) or a single asciinema/GIF. Store these under `adam-agent/captures/`.

---

## Style

- Strict TypeScript. No `any`. Prefer inferred types.
- Small files. No file over 150 lines.
- No comments unless the code genuinely needs them.
- Match the AI SDK's idiomatic patterns — do not reinvent the tool-calling or approval mechanism.
