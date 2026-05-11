# Introduction to AI SDK and Ink: Building Web and Terminal Apps with TypeScript

**Event:** PhUSE SDE 2026
**Session:** 13:30–14:00 (30 minutes)
**Speaker:** Yong Cao, Phastar
**Audience:** SAS programmers, statisticians, clinical programming professionals

---

## Goals

- Give a SAS/stats audience a mental model of React without assuming any frontend background
- Show why Ink (React in the terminal) is a fast path to building useful internal tools
- Introduce the Vercel AI SDK and the problems it solves for app developers
- Demonstrate a working terminal app that combines Ink and the AI SDK

---

## Outline

### 0. Setup: why TypeScript (≈30 sec, no dedicated slide)

A brief acknowledgment woven into the opening — not a standalone section.

- Nod to the audience: Python is the more familiar language in the stats world
- Why TypeScript here: it is one of the very few mainstream languages that runs natively across **browser, server, and terminal** — built on JavaScript, but with the type system that makes larger apps maintainable
- This versatility is exactly what makes today's talk possible: the same language powers the web app *and* the terminal app in the title
- Natural bridge into Section 1: "and that 'runs everywhere' story starts with React"

*To fill in: the exact one-liner. Current draft — "Python may be more familiar in our world; I'm using TypeScript today because it's one of the few languages that runs in the browser, on a server, and in a terminal — and you'll see all three today."*

---

### 1. Opening: React through a SAS lens (≈2 min)

Two analogies, delivered back-to-back, to bring the audience into the frontend world. These are the "hooks" of the talk — the most important 90 seconds.

#### Analogy 1 — Component ≈ SAS macro

**Speaker line:**
> *"If you've written a SAS macro — `%macro table1(dataset=, treatment=)` — you've already written a component. You defined inputs, you used it inside bigger programs, you reused it across studies. React components are the same idea, applied to UI."*

Key points on the slide:
- Both take parameters
- Both nest inside larger pieces
- Both exist to be reused
- Difference: a macro returns SAS code; a component returns UI

#### Analogy 2 — Renderer abstraction ≈ PROC REPORT + ODS

**Speaker line:**
> *"You already know this pattern. You write PROC REPORT once, and ODS sends it to RTF, PDF, or HTML. React is the same: you write a component once, and a renderer sends it to the browser, to mobile — or, with Ink, to the terminal. Ink is just another ODS destination."*

Key points on the slide:
- PROC REPORT defines *what* the report is; ODS decides *how* it's rendered (RTF / PDF / HTML)
- A React component defines *what* the UI is; a renderer decides *where* it runs (DOM / Ink / Native)
- The last sentence doubles as the transition into Section 2 — no extra bridge needed

*Delivery note: A2 lands first because it gives the audience a concrete picture they already own (a `table1` macro). B2 lands second because it's the structural claim that justifies the rest of the talk.*


---

### 2. Ink: React in the terminal (≈4 min)

- Ink is "React with a terminal renderer" — same mental model, different output target
- Why terminal apps fit our world:
  - Run locally → direct access to spec files, skill libraries, SAS datasets, existing CLI tools (foreshadowing the demo: the agent reads a local spec and a local best-practices file, then writes a `.sas` file next to them)
  - Constrained UI surface → fewer design decisions, less time on CSS/layout
  - Fast iteration → ideal for internal tools and prototypes

*To fill in: one short Ink snippet or screenshot.*

---

### 3. Bridge: from UI to AI (≈1 min)

- We now have a way to build a terminal UI quickly
- Next question: how do we give it intelligence?
- One-line transition into the AI SDK

*To fill in: the exact bridging sentence.*

---

### 4. AI SDK: what it is and what it solves (≈3 min)

- The problem the AI SDK solves for developers:
  - Different model providers have different APIs, streaming formats, tool-calling conventions
  - The AI SDK gives a single TypeScript interface across providers
- Two pieces, at a glance:
  - **AI SDK Core** — provider-agnostic model calls, streaming, tools
  - **AI SDK UI** — headless, framework-agnostic UI primitives (works in web *and* terminal)

*To fill in: a concrete "before/after" showing what the AI SDK removes.*

---

### 5. The three concepts that matter for the demo (≈4 min)

Each concept is introduced using one of the tools from the demo agent (Section 6) — no throwaway examples.

- **Streaming output** — anchor tool: `adam_plan`
  - The plan is several paragraphs of markdown; showing it token-by-token is both a real UX need and the most visible "aha" moment for the audience
  - Contrast: wait 15 seconds staring at a blank screen vs. watch the plan build itself line by line
- **Tools** — anchor tool: `read_spec`
  - Simplest tool to explain: structured input (spec path), structured output (dataset metadata, variables, derivations)
  - Teaching point: the model doesn't parse the spec — our code does; the model decides *when* to call it
- **Tool Approval** — anchor tool: `gen_program`
  - Only the tool that writes to disk needs approval; `read_spec`, `read_skill`, `adam_plan` are read-only or pure-text
  - SAS-world parallel: like the difference between `PROC PRINT` and `PROC SQL ... DELETE` — not all operations deserve the same level of trust
  - This is the teaching point, not just a safety feature

*To fill in: one short code sketch per concept, ideally pulled directly from the demo source.*

---

### 6. Demo: an ADaM agent built with Ink + AI SDK (≈10 min)

A terminal app where a user points the agent at an ADaM spec and walks away with a draft SAS program. The agent has four tools; together they form the narrative spine of the whole talk.

#### The four tools

| Tool | Input | Output | Side effects | Role in the talk |
|---|---|---|---|---|
| `read_spec` | Path to spec file | Structured spec: dataset name, label, structure, key variables, classification (ADSL / BDS / OCCDS / OTHER), all variables; for BDS, parameter-level derivation and per-variable derive flags | None (read-only) | Anchor for "Tools" concept |
| `read_skill` | Dataset type (`ADSL` / `BDS` / `OCCDS` / `OTHER`) | Contents of the matching local skill file — SAS best-practice patterns for that domain and scenario | None (read-only) | Shows the terminal-app superpower: local files as knowledge |
| `adam_plan` | Structured spec | A markdown plan: what the program should do, step by step, no code | None (text only) | Anchor for "Streaming" concept |
| `gen_program` | Plan + skill + dataset type | Draft SAS program | **Writes `.sas` file to disk** | Anchor for "Tool Approval" concept |

#### Why a separate `read_skill` tool

- Skills live as local markdown files (e.g. `skills/adsl.md`, `skills/bds.md`) that the team can edit without touching the agent code
- Splitting `read_skill` out of `gen_program` makes the data flow visible on screen: the audience literally sees the agent fetch the best-practice file before writing code
- Reinforces the terminal-app value proposition from Section 2

#### Full agent flow (three acts + coda)

**Act 1 — ADSL: the familiar case (≈2 min)**
- User: *"Generate an ADSL program from `specs/adsl.xlsx`"*
- Agent calls `read_spec("specs/adsl.xlsx")` → returns structured spec, classified as ADSL
- Ink UI shows the parsed spec in a compact panel: dataset, key vars, variable count
- Teaching beat: *"This is a tool call. The model didn't parse Excel — our code did. The model decided when to ask for it."*

**Act 2 — The plan, streamed (≈3 min)**
- Agent calls `read_skill("ADSL")` to load the ADSL best-practice file (brief on-screen flash)
- Agent calls `adam_plan(spec, skill)` — plan streams into the UI line by line
- Teaching beat: *"This is streaming. Same token-by-token UX you know from ChatGPT, but rendered by Ink inside our terminal."*

**Act 3 — Generating code, with a gate (≈4 min)**
- Agent calls `gen_program(plan, skill, "ADSL")`
- **Tool Approval prompt** appears in Ink: *"About to write `output/adsl.sas` (132 lines). Approve? [y/N]"*
- **Reject once on purpose** — show the agent gracefully handling the refusal
- Re-run and approve — file is written; `cat output/adsl.sas` (or an Ink diff view) shows the result
- Teaching beat: *"`read_spec` and `read_skill` are read-only, so no prompt. `gen_program` writes to disk, so it earns a prompt. Tool Approval is about side effects, not about AI."*

**Coda — BDS, to show it scales (≈1 min)**
- Switch target to `specs/adlb.xlsx`
- Call `read_spec` only — show the BDS-specific output: parameter list, per-parameter derivations, per-variable derive flags
- Do NOT run `gen_program` — just close with: *"Same agent, same four tools, more complex spec. This is the shape of a real internal tool."*

#### Presentation format note

The demo will most likely **not** be run live on stage — instead, screenshots or short animated GIFs / asciinema recordings will be embedded in the slides. This means:

- The agent itself still needs to be real and working (screenshots must come from actual runs)
- Every visual beat above (parsed spec panel, streamed plan, approval prompt, rejection state, written file) should be captured as a separate image or GIF during a clean recording session
- Since there's no live execution risk, the slide deck can show more detail (e.g. the full approval prompt with actual file path and line count) without worrying about demo failure
- One backup live run is still worth preparing in case a question requires it, but it's not the primary delivery

*To fill in: the concrete spec files, skill file contents, and exact agent prompt.*

---

### 7. Wrap-up and Q&A (≈3 min)

- Recap: SAS macro → React component; PROC REPORT + ODS → React renderers; Ink + AI SDK → intelligent local tools
- Where to go next (links, repos)
- Q&A

*To fill in: closing line and resource list.*

---

## Open questions for the speaker

- The session title includes "Web and Terminal Apps" but the current outline is terminal-only. Add a brief web comparison, or adjust the title?
- Is there a specific clinical/stats scenario the demo should target (e.g., reading an ADaM dataset, summarizing a log) so the audience sees immediate relevance?
- Tool Approval: shown only inside the demo, or called out as its own slide?

---

## Handoff notes for the PPT agent (to be refined)

- Slide density should stay low — this is a 30-minute talk with a live demo
- Every React/AI concept should be anchored to a SAS or clinical-programming reference point where possible
- Keep code snippets short; prefer one idea per slide

