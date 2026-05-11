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

**Speaker line (final):**
> *"Python is probably the language most of you reach for day to day. Today I'm using TypeScript — because it's one of the few languages that runs in the browser, on a server, and in a terminal, and you'll see all three today. That 'runs everywhere' story is what makes the rest of this talk possible."*

Why this works:
- Meets the audience where they are (acknowledges Python's dominance in stats)
- Pitches TS's **reach** rather than its type system — reach directly maps to the "Web and Terminal" in the title
- The last sentence is the natural bridge into Section 1

*No slide. Delivered verbally as part of the opening, right before "React through a SAS lens."*

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

Three beats: what Ink is, why the terminal is a good fit for our world, and a tiny snippet to prove it.

#### Beat 1 — What Ink is (≈30 sec)

**Speaker line:**
> *"Ink is the terminal destination. Same React you'd write for a web page — components, props, state — but it renders into boxes of text instead of HTML elements. Flexbox layout, keyboard input, all of it, in your terminal."*

Slide: one split image — a React web component next to the same-shape Ink component, with `div/span` on the left and `Box/Text` on the right.

#### Beat 2 — Why terminal apps fit our world (≈2 min)

Three reasons, one line each.

- **Runs locally.** Direct access to spec files, skill libraries, SAS datasets, existing CLI tools. No CORS, no upload/download, no "can I reach your server?" — the demo's agent reads a local spec and writes a `.sas` file next to it.
- **Constrained UI surface.** Text and boxes, not a blank canvas. Fewer design decisions, no CSS, no responsive breakpoints. You spend your time on logic, not layout.
- **Fast iteration.** The two points above compress the "from idea to working tool" loop. An afternoon gets you a real internal prototype you can hand to a colleague over `npm link`.

Slide: three icons + one-line captions. No paragraph text.

#### Beat 3 — A tiny snippet (≈1 min)

Show the smallest believable Ink program — a counter or a streaming log — so the audience sees JSX rendering to the terminal with their own eyes.

```tsx
import { render, Box, Text, useInput } from 'ink';
import { useState } from 'react';

function Counter() {
  const [n, setN] = useState(0);
  useInput((input) => {
    if (input === '+') setN(n + 1);
  });
  return (
    <Box borderStyle="round" paddingX={1}>
      <Text>Count: <Text color="cyan">{n}</Text>  (press +)</Text>
    </Box>
  );
}

render(<Counter />);
```

**Speaker line over the snippet:**
> *"Hooks, JSX, props, state. The mental model you'd have for a web page, pointed at a terminal. That's all Ink is."*

Closing beat: *"Now we have the UI half. Let's talk about the intelligence half."* → bridges into Section 3.

*To fill in (optional): one screenshot of the counter running, for the slide.*

---

### 3. Bridge: from UI to AI (≈1 min)

One line to carry the audience from "we can build a terminal UI fast" to "now let's make it smart."

**Speaker line:**
> *"So we have a way to build a terminal UI in an afternoon. The question is: how do we make it useful for the kind of work we actually do? That's where the AI SDK comes in."*

No slide transition tricks — this is a single sentence between two section slides.

---

### 4. AI SDK: what it is and what it solves (≈3 min)

Three beats: the problem, Core, UI. The UI beat is where the talk's title ("Web **and** Terminal Apps") gets paid off.

#### Beat 1 — The problem (≈1 min)

**Speaker line:**
> *"If you've tried to call an LLM from code, you've noticed: every provider is different. Anthropic, OpenAI, Google, Bedrock, Azure — different request formats, different streaming protocols, different tool-calling conventions. Swap a provider and you rewrite."*

Slide: a side-by-side of two provider SDKs with the same intent expressed differently. Caption: *"This is the problem."*

#### Beat 2 — AI SDK Core (≈1 min)

**Speaker line:**
> *"AI SDK Core is one TypeScript interface across all of them. `streamText`, `generateText`, `tool()` — same function, you change a model string instead of rewriting your code."*

Slide: one short code block showing `streamText({ model: anthropic("claude-sonnet-4-6"), ... })` with the `model:` line highlighted. Subtext: *"Change this line, keep everything else."*

#### Beat 3 — AI SDK UI (≈1 min) — *title payoff*

**Speaker line:**
> *"AI SDK UI is the other half. It's **headless** — no components, just hooks and state machines for chat, streaming, and tool approvals. Headless means you bring your own rendering. On the web, React on the DOM. In the terminal, React with Ink. **Same hooks, same patterns, two targets.** That's what the title meant by 'Web and Terminal Apps'."*

Slide: the same `useChat`-style hook rendered twice — once into `<div>` (web), once into `<Box>` (Ink). This is the single most important visual in the talk.

*To fill in: the two side-by-side rendering snippets.*

---

### 5. The three concepts that matter for the demo (≈4 min)

Each concept is introduced using one of the tools from the demo agent (Section 6) — no throwaway examples. All snippets are lifted directly from the demo source.

#### Streaming — anchor tool: `adam_plan` (≈1 min 20 sec)

**Speaker line:**
> *"The plan is several paragraphs of markdown. You could wait 15 seconds and show it all at once — or you could stream it. Same API call, one line different."*

```ts
const { textStream } = streamText({
  model: anthropic('claude-sonnet-4-6'),
  prompt: buildPlanPrompt(spec, skill),
});

for await (const chunk of textStream) {
  appendToPlan(chunk);   // Ink re-renders on each chunk
}
```

Teaching beats:
- The `for await` loop is the whole trick — tokens arrive, UI updates
- Ink's reactivity is what makes this feel native (no manual repainting)
- Contrast the UX: *blank screen for 15 sec* vs *plan builds itself line by line*

#### Tools — anchor tool: `read_spec` (≈1 min 20 sec)

**Speaker line:**
> *"The model doesn't parse Excel. Our code does. The model decides **when** to call it — that's the whole idea of a tool."*

```ts
const readSpec = tool({
  description: 'Parse a Pinnacle 21 ADaM spec file',
  inputSchema: z.object({ path: z.string() }),
  execute: async ({ path }) => {
    return parseP21Workbook(path);   // plain TS, no AI involved
  },
});

streamText({ model, tools: { read_spec: readSpec }, prompt: userMessage });
```

Teaching beats:
- `inputSchema` is the contract — the model can only call it with a valid shape
- `execute` is just a TypeScript function; the AI never touches the xlsx bytes
- The model sees the tool's description and decides when to invoke it

#### Tool Approval — anchor tool: `gen_program` (≈1 min 20 sec)

**Speaker line:**
> *"`read_spec` and `read_skill` are read-only, so they run immediately. `gen_program` writes to disk — so it earns a prompt. Tool Approval is about **side effects**, not about AI."*

```ts
const genProgram = tool({
  description: 'Write a draft SAS program to disk',
  inputSchema: z.object({
    plan: z.string(),
    skill: z.string(),
    datasetType: z.string(),
    outputPath: z.string(),
  }),
  needsApproval: true,                         // <-- the whole difference
  execute: async (input) => writeSasFile(input),
});
```

Teaching beats:
- One flag — `needsApproval: true` — converts a tool into a gated tool
- The SDK pauses the loop and surfaces the pending call to the UI; the UI (Ink) renders the prompt
- SAS-world parallel: like the difference between `PROC PRINT` (safe) and `PROC SQL ... DELETE` (gated) — not all operations deserve the same trust
- **This is the real point:** the gate lives in your code, not in the model

*Delivery note: each of the three blocks fits on one slide. The code is short on purpose — the speaker line does the work, the code proves it.*

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

One slide to recap the talk's through-line, one slide for resources, then Q&A.

#### Recap slide

The whole talk is one idea at three altitudes. The recap slide says it in three lines:

- **Language:** TypeScript — one language, browser + server + terminal
- **Framework:** React — one component model, DOM + Ink + Native (like PROC REPORT + ODS)
- **Intelligence:** AI SDK — one interface, any provider; headless UI, web + terminal

**Speaker line:**
> *"Same story, three altitudes. Learn it once, use it in the browser, on the server, and in the terminal. That's what lets you build an internal tool like today's demo in an afternoon."*

#### Resources slide

- **Ink** — `github.com/vadimdemedes/ink`
- **Vercel AI SDK** — `ai-sdk.dev` (docs), `github.com/vercel/ai`
- **Today's demo code** — *repo link to be added*
- **Slides & notes** — *link to be added*
- **Contact** — Yong Cao, Phastar

#### Q&A posture

- Expect questions on: regulatory / validation concerns, hallucination risk, how this fits next to existing macro libraries, running without internet, cost per run
- Prepared answers live in a separate speaker-notes doc (not in the slide deck)
- If a question requires a live run, the demo app is ready on the laptop as a backup

*To fill in: final repo and slides URLs; exact wording of the one-line closer before Q&A.*

---

## Open questions for the speaker

Most of the original open questions were resolved while drafting the sections. Only one decision is still outstanding:

- **Keep the BDS coda in the demo (Section 6)?** Showing `read_spec` on an ADLB spec at the end demonstrates the architecture scales, but it costs ~1 minute. If the talk runs long in rehearsal, this is the first thing to cut and replace with a tighter jump to the recap.

Decisions already made (recorded here for the PPT agent's reference):

- **Web vs Terminal scope** — paid off in Section 4 Beat 3 via the AI SDK UI "same hooks, two targets" slide; no separate web demo needed.
- **Tool Approval placement** — discussed conceptually in Section 5 (`needsApproval: true` snippet), demonstrated visually in Section 6 Act 3; no dedicated standalone slide.
- **Demo scenario** — ADaM agent with four tools (`read_spec`, `read_skill`, `adam_plan`, `gen_program`) over Pinnacle 21 specs; full spec in Section 6 and in `demo-app-prompt.md`.
- **Live vs recorded demo** — captured as screenshots / GIFs embedded in slides; not run live. Speaker keeps the built app on the laptop as a Q&A backup.

---

## Handoff notes for the PPT agent

**Deck shape**

- Total runtime: 30 minutes, including Q&A. Target ≈25 minutes of speaking + 5 min Q&A.
- Estimated slide count: 18–22. Section map:
  - Title + speaker intro: 1 slide
  - Section 0 (TypeScript): **no slide** — verbal only
  - Section 1 (React analogies): 2 slides (one per analogy)
  - Section 2 (Ink): 3 slides (what Ink is, why terminal, counter snippet)
  - Section 3 (bridge): **no slide** — verbal transition
  - Section 4 (AI SDK): 3 slides (the problem, Core, UI with the side-by-side web/terminal code)
  - Section 5 (three concepts): 3 slides (one per concept, each with a code block)
  - Section 6 (demo): 4–6 slides built from screenshots/GIFs (parsed spec → streamed plan → approval prompt → rejection state → written file → optional BDS coda)
  - Section 7 (wrap-up): 2 slides (recap, resources)

**Visual priorities**

- **Most important visual:** Section 4 Beat 3 — `useChat`-style hook rendered once into `<div>` (web) and once into `<Box>` (Ink), side by side. This single slide pays off the talk title.
- **Second most important:** Section 6 approval prompt screenshot — this is the "Tool Approval" moment the audience remembers.
- **Third:** Section 2 counter snippet rendered in the terminal — first proof that JSX really runs in a terminal.

**Style rules**

- Low density: at most one idea per slide. Many slides will be a speaker line + one short code block or one image.
- Every code block is short (≤ 10 lines visible). Longer logic lives in the demo repo, not on screen.
- Every AI/React concept is anchored to a SAS or clinical-programming reference point where it exists; never introduce a frontend term without a bridge.
- Use one accent color consistently (cyan or green); red reserved for the rejection state in Section 6.
- No em dashes in slide text — the speaker notes use them, but slides use short phrases.

**Inputs for the PPT agent**

- This file (`talk-outline.md`) is the source of truth for content and section order.
- `demo-app-prompt.md` is the source of truth for the demo code and the screenshots that will be embedded in Section 6.
- Speaker lines marked with `>` in each section should appear in the slide notes (for the speaker), not on the slide itself.
- When generating code slides, pull snippets from the demo repo rather than paraphrasing the sketches in this outline.

