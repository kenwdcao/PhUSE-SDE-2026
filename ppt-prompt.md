# All-In-One PowerPoint Generation Prompt

You are a senior presentation designer, technical storyteller, and PowerPoint production agent.

Create a complete, polished, editable PowerPoint deck for a 30-minute conference session at **PhUSE SDE 2026**.

This prompt is self-contained. Do not ask for `talk-outline.md`, `demo-app-prompt.md`, source files, or local screenshots. If the user later uploads real screenshots or GIFs, use them. Otherwise, create high-fidelity editable terminal mockups based on the details below.

The visible slide text must be in **English**.

The speaker will present in **Chinese**, so every slide must include **Chinese speaker notes** written as natural spoken remarks.

---

## 1. Session Metadata

- **Title:** Introduction to AI SDK and Ink
- **Subtitle:** Building Web and Terminal Apps with TypeScript
- **Event:** PhUSE SDE 2026
- **Session:** 13:30-14:00, 30 minutes total
- **Speaker:** Yong Cao, Phastar
- **Audience:** SAS programmers, statisticians, statistical programmers, clinical programming professionals, and technically curious clinical development professionals
- **Talk length:** about 25 minutes speaking plus about 5 minutes Q&A
- **Main deck length:** target 20 slides, acceptable range 18-22 slides
- **Optional appendix:** 3-5 hidden backup Q&A slides are allowed if the tool supports hidden slides

---

## 2. Core Narrative

This is not a generic AI hype talk.

This is not an API reference walkthrough.

The talk introduces a practical TypeScript application stack for controlled AI tools:

1. **React through a SAS lens**
   - A React component is like a SAS macro: it takes inputs, can be nested, and is reusable.
   - A React renderer is like ODS: the same definition can be sent to different destinations.

2. **Ink**
   - Ink is React rendered in the terminal.
   - It is a fast path for internal tools close to local files, specs, scripts, and command-line workflows.

3. **AI SDK**
   - AI SDK Core gives one TypeScript interface for model calls, streaming, tools, and approval.
   - AI SDK UI is headless: it gives hooks and state machines for chat, streaming, and tool interaction, but the app brings its own rendering.
   - The same interaction pattern can render on the web with DOM or in the terminal with Ink.

4. **Demo**
   - A terminal ADaM agent reads a Pinnacle 21 spec.
   - It loads local SAS best-practice skill files.
   - It streams an implementation plan.
   - It writes a draft SAS program only after approval.

The audience should leave with this mental model:

**Learn one component model and one AI application interface, then render controlled AI workflows in the browser, on a server, or in the terminal.**

---

## 3. Language Rules

### Visible Slide Text

- English only.
- Short phrases, not paragraphs.
- One core idea per slide.
- No visible placeholder text such as "insert screenshot", "to be added", "speaker note", or "placeholder".
- No fake QR codes.
- No em dashes in visible slide text. Use colons, commas, or short sentences.
- Code may include TypeScript, JSX, SAS-style macro syntax, package names, URLs, and file paths.
- Keep visible text readable from the back of a conference room.

### Speaker Notes

- Chinese only.
- Keep technical terms in English where natural: React, Ink, AI SDK, streaming, tools, approval, TypeScript, SAS macro, ODS, ADaM, BDS.
- Write notes as natural spoken Chinese, not literal translations.
- Include click cues for animated slides, for example: `[Click] 这里先看左边...`
- When introducing a frontend concept, bridge it back to SAS or clinical programming.
- Do not over-explain in notes. The speaker has 25 minutes for the main talk.

### Required Opening Note

Include this idea in Chinese speaker notes on Slide 1 or Slide 2, but do not create a separate visible TypeScript slide:

> Python 可能是大家日常最常用的语言。今天我用 TypeScript，是因为它可以跑在浏览器、服务器和 terminal 里。这个 runs everywhere 的特性，是后面 Web and Terminal 这条线成立的原因。

---

## 4. Design Direction

Build a premium technical conference deck, not a generic corporate template.

The deck should feel like:

- clinical programming,
- terminal tooling,
- modern TypeScript development,
- controlled AI workflows,
- credible engineering, not AI spectacle.

### Format

- 16:9 widescreen.
- Editable PowerPoint objects wherever possible.
- Use raster images only for real screenshots, GIFs, generated background images, or terminal captures.
- Keep important text live/editable unless it is part of a screenshot.

### Visual System

Use a light conference theme with dark technical surfaces:

- Background: warm off-white or very light gray.
- Primary text: near-black charcoal.
- Primary accent: cyan or teal.
- Secondary accent: restrained green.
- Warning/rejection accent: red, used only for side effects, rejection, or approval gates.
- Avoid purple-dominant, beige-dominant, or dark-blue-only palettes.

Recommended palette:

- Background: `#F7F8FA`
- Text: `#111827`
- Muted text: `#5B6472`
- Divider: `#D8DEE7`
- Code panel: `#0B1220`
- Code text: `#D6E4FF`
- Cyan accent: `#00A6D6`
- Green accent: `#10B981`
- Red accent: `#E5484D`
- Soft highlight: `#E6F7FB`

### Typography

- Use a modern sans-serif such as Aptos, Inter, or IBM Plex Sans.
- Use a monospaced font such as JetBrains Mono, Cascadia Code, or IBM Plex Mono for code and terminal panels.
- Slide titles should be large and confident, but not oversized.
- Minimum readable body size: 22 pt.
- Minimum code size: 16-18 pt.
- Do not cram code. Use fewer lines rather than smaller text.

### Layout Rhythm

Use varied layouts across the contact sheet:

- Analogy slides: two-column comparison.
- Architecture slides: clean system diagrams.
- Code slides: dark code panel plus one short claim.
- Demo slides: large terminal capture or mockup with a small annotation rail.
- Recap slides: compact layered synthesis.

Avoid repeated card grids.

Do not put cards inside cards.

Do not use decorative AI robot imagery, glowing brains, stock-cloud visuals, gradient blobs, or generic "AI future" visuals.

### Code And Terminal Rendering

Code and terminal visuals are critical.

- Render code in dark editor-style panels.
- Preserve indentation and line breaks.
- Use TypeScript syntax highlighting when possible.
- Limit visible code to 10 lines per slide.
- Highlight only the line that matters.
- Use terminal panels with a title bar, prompt line, and status accents.
- Terminal app states should look like real software, not generic black boxes.

### Icons And Diagrams

Use simple line icons only where they clarify scanning:

- file icon for local spec,
- terminal icon for Ink,
- browser window for DOM,
- lock/check for approval,
- stream/wave for streaming,
- wrench/tool for tool calls.

Diagrams should show direction and state changes.

### Accessibility

- High contrast.
- Do not rely on color alone.
- Every diagram label should be readable at thumbnail size.
- Avoid dense tables.

---

## 5. Animation And Interaction Direction

Use animation to explain mechanisms, not as decoration.

Default animation:

- Fade or appear.
- On click.
- 0.2-0.5 seconds.
- No bounce, spin, excessive zoom, or random transitions.

Use a consistent visual language:

- **Reveal:** introduce the next concept.
- **Flow:** move request/data left to right.
- **Stream:** show text arriving chunk by chunk.
- **Gate:** pause at an approval boundary.
- **Resolve:** show approved or rejected outcome.

### Required Animated Moments

1. **Renderer analogy**
   - Show `PROC REPORT`.
   - Reveal ODS destinations: RTF, PDF, HTML.
   - Reveal React destinations: DOM, Ink, Native.
   - End with: **Ink is another rendering destination.**

2. **AI SDK UI payoff**
   - Show one `useChat`-style hook in the center.
   - On click, split into two targets:
     - Web: `<div>`
     - Terminal: `<Box>` / `<Text>`
   - This is the most important slide in the deck.

3. **Streaming**
   - Do not show the whole response at once.
   - Animate 3-4 chunks appearing line by line inside a terminal panel.
   - Tie it to `adam_plan`.

4. **Tools**
   - Animate: model decides -> schema validates -> TypeScript function executes -> result returns.
   - Make clear that the model does not parse Excel; code parses Excel.

5. **Approval**
   - Animate `gen_program` reaching an approval gate.
   - Pause at the prompt.
   - On click, show rejection branch.
   - On click, show approval branch.
   - The remembered idea: approval is about side effects.

6. **Demo**
   - Prefer embedded GIFs or staged click builds for plan streaming and approval.
   - The deck must still work as static slides if animation fails.

---

## 6. Talk Content Source

Use this section as the complete source material for the deck.

### Opening: Why TypeScript

No dedicated slide.

Speaker should say this near the opening:

> Python is probably the language most of you reach for day to day. Today I'm using TypeScript because it's one of the few languages that runs in the browser, on a server, and in a terminal, and you'll see all three today. That "runs everywhere" story is what makes the rest of this talk possible.

Purpose:

- Meet the audience where they are.
- Do not position TypeScript against Python.
- Emphasize reach across browser, server, and terminal.

### Section 1: React Through A SAS Lens

Two analogies are the hook for the talk.

#### Analogy 1: Component Is Like SAS Macro

Speaker idea:

> If you've written a SAS macro such as `%macro table1(dataset=, treatment=)`, you've already written a component. You defined inputs, used it inside bigger programs, and reused it across studies. React components are the same idea, applied to UI.

Visible slide points:

- Both take parameters.
- Both nest inside larger pieces.
- Both exist to be reused.
- Difference: a macro returns SAS code; a component returns UI.

#### Analogy 2: Renderer Is Like PROC REPORT Plus ODS

Speaker idea:

> You already know this pattern. You write PROC REPORT once, and ODS sends it to RTF, PDF, or HTML. React is the same: you write a component once, and a renderer sends it to the browser, to mobile, or with Ink, to the terminal. Ink is just another ODS destination.

Visible slide points:

- PROC REPORT defines what the report is.
- ODS decides how it is rendered: RTF, PDF, HTML.
- React component defines what the UI is.
- Renderer decides where it runs: DOM, Ink, Native.

### Section 2: Ink, React In The Terminal

#### Beat 1: What Ink Is

Speaker idea:

> Ink is the terminal destination. Same React you would write for a web page: components, props, state. But it renders into boxes of text instead of HTML elements. Flexbox layout, keyboard input, all of it, in your terminal.

Visible points:

- React component model.
- Terminal text and boxes.
- Flexbox layout.
- Keyboard input.

Visual:

- Split image or diagram:
  - Web React: `div`, `span`
  - Ink React: `Box`, `Text`

#### Beat 2: Why Terminal Apps Fit This World

Visible points:

- **Runs locally:** direct access to spec files, skill libraries, SAS datasets, existing CLI tools.
- **Constrained UI:** text and boxes, fewer design decisions, no CSS rabbit hole.
- **Fast iteration:** idea to prototype can be an afternoon.

Speaker emphasis:

- No CORS.
- No upload/download cycle.
- No "can I reach your server?"
- Demo agent reads a local spec and writes a `.sas` file next to it.

#### Beat 3: Tiny Ink Snippet

Use this code:

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

For the slide, shorten if necessary:

```tsx
function Counter() {
  const [n, setN] = useState(0);
  useInput(input => {
    if (input === '+') setN(n + 1);
  });
  return <Text>Count: {n}</Text>;
}
```

Speaker idea:

> Hooks, JSX, props, state. The mental model you would have for a web page, pointed at a terminal. That's all Ink is.

Bridge:

> Now we have the UI half. Let's talk about the intelligence half.

### Section 3: Bridge From UI To AI

No dedicated slide.

Speaker transition:

> So we have a way to build a terminal UI in an afternoon. The question is: how do we make it useful for the kind of work we actually do? That's where the AI SDK comes in.

### Section 4: AI SDK, What It Solves

#### Beat 1: Provider Fragmentation

Speaker idea:

> If you've tried to call an LLM from code, you've noticed: every provider is different. Anthropic, OpenAI, Google, Bedrock, Azure, different request formats, different streaming protocols, different tool-calling conventions. Swap a provider and you rewrite.

Visible points:

- Different request formats.
- Different streaming protocols.
- Different tool conventions.
- Same intent, different interfaces.

Visual:

- Side-by-side provider SDK cards.
- Keep code schematic unless verified.

#### Beat 2: AI SDK Core

Speaker idea:

> AI SDK Core is one TypeScript interface across all of them. `streamText`, `generateText`, `tool()`, same function, and you change a model string instead of rewriting your code.

Use a short code panel like:

```ts
const result = streamText({
  model: anthropic('claude-sonnet-4-6'),
  prompt,
  tools,
});
```

Highlight:

- `model: ...`
- `streamText`
- `tools`

#### Beat 3: AI SDK UI

This is the title payoff slide.

Speaker idea:

> AI SDK UI is the other half. It is headless: no components, just hooks and state machines for chat, streaming, and tool approvals. Headless means you bring your own rendering. On the web, React on the DOM. In the terminal, React with Ink. Same hooks, same patterns, two targets.

Visible points:

- Headless interaction state.
- Web renders DOM.
- Ink renders terminal UI.
- Same hooks, same patterns, two targets.

Visual:

Center:

```tsx
const chat = useChat();
```

Left:

```tsx
return (
  <div>
    {chat.messages.map(m => (
      <p>{m.text}</p>
    ))}
  </div>
);
```

Right:

```tsx
return (
  <Box flexDirection="column">
    {chat.messages.map(m => (
      <Text>{m.text}</Text>
    ))}
  </Box>
);
```

### Section 5: Three Concepts That Matter For The Demo

Each concept should use one tool from the demo. No throwaway examples.

#### Concept 1: Streaming, Anchor Tool `adam_plan`

Speaker idea:

> The plan is several paragraphs of markdown. You could wait 15 seconds and show it all at once, or you could stream it. Same API call, one line different.

Use this code:

```ts
const { textStream } = streamText({
  model,
  prompt: buildPlanPrompt(spec, skill),
});

for await (const chunk of textStream) {
  appendToPlan(chunk);
}
```

Teaching beats:

- The `for await` loop is the whole trick.
- Tokens arrive, UI updates.
- Ink reactivity makes it feel native.
- Contrast blank screen vs plan building line by line.

#### Concept 2: Tools, Anchor Tool `read_spec`

Speaker idea:

> The model does not parse Excel. Our code does. The model decides when to call it. That's the whole idea of a tool.

Use this code:

```ts
const readSpec = tool({
  description: 'Parse a Pinnacle 21 ADaM spec file',
  inputSchema: z.object({ path: z.string() }),
  execute: async ({ path }) => {
    return parseP21Workbook(path);
  },
});
```

Teaching beats:

- `inputSchema` is the contract.
- The model can only call it with a valid shape.
- `execute` is just TypeScript.
- The AI never touches the raw xlsx bytes.

#### Concept 3: Tool Approval, Anchor Tool `gen_program`

Speaker idea:

> `read_spec` and `read_skill` are read-only, so they run immediately. `gen_program` writes to disk, so it earns a prompt. Tool Approval is about side effects, not about AI.

Use this code:

```ts
const genProgram = tool({
  description: 'Write a draft SAS program to disk',
  inputSchema: z.object({
    plan: z.string(),
    skill: z.string(),
    datasetType: z.string(),
    outputPath: z.string(),
  }),
  needsApproval: true,
  execute: async (input) => writeSasFile(input),
});
```

Teaching beats:

- One flag converts the tool into a gated tool.
- The SDK pauses the loop and surfaces the pending call to the UI.
- The UI renders the prompt.
- SAS-world parallel: safe read-only actions should not be treated the same as write/delete actions.
- The gate lives in your code, not in the model.

### Section 6: Demo, ADaM Agent Built With Ink And AI SDK

The demo will most likely not run live on stage. The deck should use screenshots, GIFs, asciinema captures, or high-fidelity mockups.

The demo is a terminal app where a user points the agent at an ADaM spec and walks away with a draft SAS program.

#### Demo Stack

- Runtime: Node.js 20+ or Bun.
- Language: TypeScript.
- UI: Ink.
- AI: Vercel AI SDK.
- Validation: zod.
- Spec parsing: xlsx / SheetJS.

#### Demo User Request

```text
Generate an ADSL program from specs/adsl.xlsx and write it to output/adsl.sas.
```

#### Agent System Prompt

```text
You are an ADaM programming assistant. When given a spec path, your job is to:
1. Call read_spec to understand the dataset.
2. Call read_skill for that dataset's class.
3. Call adam_plan to produce a step-by-step plan.
4. Call gen_program to write a draft SAS program.
Always call the tools in order. Do not write code yourself.
```

#### The Four Demo Tools

1. `read_spec`
   - Input: `{ path: string }`
   - Output:
     - dataset name, e.g. `ADSL`
     - label
     - class: `ADSL`, `BDS`, `OCCDS`, or `OTHER`
     - structure
     - key variables
     - variable list
     - for BDS, parameter-level derivations
   - Side effects: none
   - Teaching role: Tools concept

2. `read_skill`
   - Input: `{ datasetType: "ADSL" | "BDS" | "OCCDS" | "OTHER" }`
   - Output: local markdown skill file content plus file path
   - Side effects: none
   - Teaching role: terminal apps can use local files as knowledge

3. `adam_plan`
   - Input: `{ spec: DatasetSpec; skill: string }`
   - Output: streamed markdown implementation plan
   - Side effects: none
   - Teaching role: Streaming concept

4. `gen_program`
   - Input: `{ plan: string; skill: string; datasetType: string; outputPath: string }`
   - Output: `{ path: string; lineCount: number }`
   - Side effect: writes a `.sas` file
   - Approval required
   - Teaching role: Tool Approval concept

#### Demo Flow

Act 1: ADSL, the familiar case

- User asks for an ADSL program from `specs/adsl.xlsx`.
- Agent calls `read_spec("specs/adsl.xlsx")`.
- Output is structured spec, classified as ADSL.
- Ink UI shows a compact panel:
  - dataset: ADSL,
  - key variables,
  - structure,
  - variable count.
- Teaching beat: this is a tool call. The model did not parse Excel; TypeScript code did.

Act 2: The plan streams

- Agent calls `read_skill("ADSL")`.
- Agent calls `adam_plan(spec, skill)`.
- Plan streams into the UI line by line.
- Teaching beat: this is streaming, the same token-by-token UX as ChatGPT, rendered by Ink inside the terminal.

Act 3: Generating code with a gate

- Agent calls `gen_program(plan, skill, "ADSL")`.
- Tool Approval prompt appears:

```text
About to write output/adsl.sas (132 lines). Approve? [y/N]
```

- Reject once on purpose.
- App handles rejection gracefully and does not write the file.
- Re-run and approve.
- File is written.
- Show `cat output/adsl.sas` or an Ink diff/code preview.
- Teaching beat: `read_spec` and `read_skill` are read-only, no prompt. `gen_program` writes to disk, so it earns a prompt.

Coda: BDS, to show the pattern scales

- Switch target to `specs/adlb.xlsx`.
- Call `read_spec` only.
- Show BDS-specific output:
  - parameter list,
  - per-parameter derivations,
  - per-variable derive flags.
- Do not run `gen_program`.
- Close with: same agent, same four tools, more complex spec.

#### Demo Terminal UI Requirements

Terminal visuals should include:

- Persistent top bar with app name and current dataset.
- Main panel changes states:
  - idle,
  - spec parsed,
  - plan streaming,
  - approval prompt,
  - rejection,
  - program written.
- Streamed plan renders with visible line-by-line arrival.
- Approval prompt is a distinct framed panel with `[Y]es / [N]o`.
- Use one accent color, cyan or green.
- Red only for rejection.
- Wrap text cleanly at 100 columns.

#### Suggested Mock Terminal Text

Parsed spec panel:

```text
ADaM Agent                                  dataset: ADSL

Tool call: read_spec("specs/adsl.xlsx")

Dataset      ADSL
Label        Subject-Level Analysis Dataset
Class        ADSL
Structure    One record per subject
Key vars     STUDYID, USUBJID
Variables    21

Status       Spec parsed by TypeScript
```

Plan streaming panel:

```text
ADaM Agent                                  dataset: ADSL

Tool call: adam_plan(spec, skill)

Plan
1. Read source demographics and exposure inputs.
2. Derive treatment variables TRT01P and TRT01A.
3. Apply date imputation rules from the ADSL skill.
4. Create baseline flags and safety population indicators.
```

Approval prompt:

```text
ADaM Agent                                  dataset: ADSL

Tool call pending: gen_program

About to write:
output/adsl.sas

Estimated size: 132 lines
Approve? [y/N]
```

Rejection state:

```text
Tool call rejected by user.
No file was written.
```

Approved state:

```text
Approved.
Wrote output/adsl.sas
132 lines
```

SAS preview:

```sas
data adam.adsl;
  set source.dm;
  length TRT01P TRT01A $40;
  STUDYID = strip(STUDYID);
  USUBJID = catx('-', STUDYID, SUBJECT);
run;
```

### Section 7: Wrap-Up And Q&A

Recap idea:

> Same story, three altitudes. Learn it once, use it in the browser, on the server, and in the terminal. That's what lets you build an internal tool like today's demo in an afternoon.

Visible recap:

- **Language:** TypeScript, one language for browser, server, terminal.
- **Framework:** React, one component model for DOM, Ink, Native.
- **Intelligence:** AI SDK, one interface for providers, streaming, tools, approval.

Resources:

- Ink: `github.com/vadimdemedes/ink`
- AI SDK: `ai-sdk.dev`
- Demo code: add speaker's repo link if provided; otherwise say `Demo code`
- Slides and notes: add speaker's link if provided; otherwise say `Slides and notes`
- Contact: Yong Cao, Phastar

Expected Q&A topics:

- regulatory and validation concerns,
- hallucination risk,
- relationship to existing SAS macro libraries,
- running without internet,
- cost per run.

---

## 7. Slide-By-Slide Plan

Create around 20 main slides. Follow this plan unless a small adjustment improves flow.

### Slide 1: Title

Visible:

- **Introduction to AI SDK and Ink**
- **Building Web and Terminal Apps with TypeScript**
- **Yong Cao, Phastar | PhUSE SDE 2026**

Visual:

- Browser window and terminal window converging into one AI application flow.
- Clean technical title.

Chinese notes:

- Opening.
- Include TypeScript setup and Python acknowledgement.
- Set expectation: this is about controlled AI applications, not AI hype.

### Slide 2: Component = SAS Macro

Title:

**A React component is like a reusable SAS macro**

Visible:

- Takes parameters.
- Fits inside larger programs.
- Reused across studies.
- Macro returns SAS code.
- Component returns UI.

Visual:

- Left code: `%macro table1(dataset=, treatment=);`
- Right code: `function Table1({ dataset, treatment })`
- Show inputs and reusable output.

Chinese notes:

- Use the SAS macro analogy to explain components.

### Slide 3: Renderer = ODS Destination

Title:

**React separates what you build from where it renders**

Visible:

- `PROC REPORT -> ODS -> RTF | PDF | HTML`
- `React Component -> Renderer -> DOM | Ink | Native`
- **Ink is another rendering destination.**

Visual:

- Two stacked flow diagrams.
- Highlight Ink in cyan.

Animation:

- SAS row first.
- React row second.
- Highlight Ink.

Chinese notes:

- Explain PROC REPORT and ODS, then map to React and renderers.

### Slide 4: Ink Is React In The Terminal

Title:

**Ink is React pointed at the terminal**

Visible:

- Same component model.
- Text and boxes.
- Flexbox layout.
- Keyboard input.

Visual:

- Web side: `<div>`, `<span>`.
- Terminal side: `<Box>`, `<Text>`.

Chinese notes:

- Ink is not a new mental model. It is React rendered to terminal text.

### Slide 5: Why Terminal Apps Fit This Work

Title:

**The terminal is a good home for internal tools**

Visible:

- Local files.
- Constrained UI.
- Fast iteration.

Visual:

- Three horizontal lanes:
  - spec files / skill files / SAS programs,
  - text boxes instead of blank canvas,
  - idea -> prototype -> colleague.

Chinese notes:

- Tie to specs, local scripts, CLI tools, no upload/download, fewer UI decisions.

### Slide 6: A Tiny Ink Program

Title:

**A tiny Ink app is still React**

Visible:

- Short counter code.
- Terminal output: `Count: 3 (press +)`.

Visual:

- Left code panel.
- Right terminal mockup.
- Highlight `useState` and `useInput`.

Chinese notes:

- Hooks, JSX, props, state. Same web mental model, different target.
- Bridge to AI SDK.

### Slide 7: Provider APIs Are Fragmented

Title:

**Calling an LLM is easy until you switch providers**

Visible:

- Different request formats.
- Different streaming protocols.
- Different tool conventions.
- Provider swaps can become rewrites.

Visual:

- Provider cards: OpenAI, Anthropic, Google, Bedrock, Azure.
- Caption: **Same intent, different interfaces.**

Chinese notes:

- Explain why application developers need a stable interface.

### Slide 8: AI SDK Core

Title:

**AI SDK Core gives one TypeScript interface**

Visible:

- `generateText`
- `streamText`
- `tool()`
- Change the model, keep the flow.

Visual:

- Code panel:

```ts
const result = streamText({
  model,
  prompt,
  tools,
});
```

- Swappable provider chips below.

Chinese notes:

- Explain provider-agnostic orchestration.

### Slide 9: AI SDK UI Payoff

Title:

**Headless UI means one interaction model, two render targets**

Visible:

- Same hooks.
- Same message state.
- Web renders DOM.
- Ink renders terminal UI.

Visual:

- Center: `const chat = useChat();`
- Left: web `<div>` rendering.
- Right: Ink `<Box>` and `<Text>` rendering.
- This slide must be the cleanest and most memorable slide.

Animation:

- Reveal hook first.
- Split to Web and Terminal.
- Highlight **same hooks, two targets**.

Chinese notes:

- Explain "headless": SDK gives state and behavior, app controls rendering.
- This pays off "Web and Terminal Apps".

### Slide 10: Concept 1, Streaming

Title:

**Streaming turns waiting into progress**

Visible:

- Anchor tool: `adam_plan`.
- Tokens arrive.
- Ink re-renders.
- The plan builds line by line.

Visual:

- Code panel with `textStream`.
- Terminal panel with line-by-line plan.

Animation:

- 3-4 chunks appear progressively.

Chinese notes:

- Contrast blank screen vs streamed progress.

### Slide 11: Concept 2, Tools

Title:

**Tools let the model ask your code to act**

Visible:

- Anchor tool: `read_spec`.
- Schema is the contract.
- TypeScript parses Excel.
- The model decides when to ask.

Visual:

- Flow: model -> schema -> `parseP21Workbook()` -> structured spec.

Chinese notes:

- The model does not parse Excel. Our code does.

### Slide 12: Concept 3, Approval

Title:

**Approval belongs at the side-effect boundary**

Visible:

- `read_spec`: read-only, no prompt.
- `read_skill`: read-only, no prompt.
- `gen_program`: writes to disk, approval required.

Visual:

- Gate between plan and file write.
- Use red only for side-effect warning.

Animation:

- Read-only tools pass.
- `gen_program` pauses at gate.
- Approval prompt appears.

Chinese notes:

- Approval is about side effects, not about whether AI is trusted in general.

### Slide 13: Demo Setup

Title:

**Demo: an ADaM agent in the terminal**

Visible:

- Reads a Pinnacle 21 spec.
- Loads local skill guidance.
- Streams an implementation plan.
- Writes SAS only after approval.

Visual:

- Four-tool pipeline:
  - `read_spec`
  - `read_skill`
  - `adam_plan`
  - `gen_program`
- First three marked no side effect.
- Last one marked writes `.sas`.

Chinese notes:

- Explain demo is captured, not primarily live.
- Focus on workflow shape.

### Slide 14: Demo Act 1, Parsed Spec

Title:

**Act 1: the agent reads the spec**

Visible:

- `read_spec("specs/adsl.xlsx")`
- Dataset: ADSL.
- Key variables.
- Variable count.

Visual:

- Large terminal parsed spec panel.
- Annotation rail for dataset, class, key variables.

Chinese notes:

- This is a tool call. The model asks; TypeScript parses.

### Slide 15: Demo Act 2, Plan Streaming

Title:

**Act 2: the plan streams into the terminal**

Visible:

- `read_skill("ADSL")`
- `adam_plan(spec, skill)`
- Markdown plan arrives line by line.

Visual:

- GIF or staged terminal captures.
- Mostly image-driven.

Chinese notes:

- Connect to streaming.
- Local skill files let the team update guidance without changing agent code.

### Slide 16: Demo Act 3, Approval Prompt

Title:

**Act 3: writing code earns a prompt**

Visible:

- `gen_program(plan, skill, "ADSL")`
- About to write `output/adsl.sas`.
- Approve? `[y/N]`

Visual:

- Large terminal approval prompt.
- Distinct approval gate.
- This is the second most important visual after Slide 9.

Chinese notes:

- The prompt appears because the tool writes a file.

### Slide 17: Demo Act 3, Reject Then Approve

Title:

**The app handles both paths**

Visible:

- Reject: no file written.
- Approve: draft `.sas` created.
- The gate lives in the app.

Visual:

- Two branches:
  - rejected state,
  - approved write state.
- Include small SAS preview.

Chinese notes:

- Reject once on purpose to show the control boundary.
- Then approve to show the productive path.

### Slide 18: Coda, BDS Scales The Pattern

Title:

**Same agent, more complex spec**

Visible:

- Switch to `specs/adlb.xlsx`.
- BDS classification.
- Parameter-level derivations.
- Same four-tool shape.

Visual:

- Terminal panel showing:
  - ADLB,
  - BDS,
  - HGB, WBC, PLT,
  - per-parameter derivations.

Chinese notes:

- Keep this short.
- If rehearsal runs long, this slide can be hidden.

### Slide 19: Recap

Title:

**One idea at three altitudes**

Visible:

- **Language:** TypeScript, browser + server + terminal.
- **Framework:** React, DOM + Ink + Native.
- **Intelligence:** AI SDK, streaming + tools + approval.

Visual:

- Three stacked layers.
- Show ADaM agent as resulting internal tool.

Chinese notes:

- Same story at three levels. Learn once, use across targets.

### Slide 20: Resources And Q&A

Title:

**Resources**

Visible:

- Ink: `github.com/vadimdemedes/ink`
- AI SDK: `ai-sdk.dev`
- Demo code
- Slides and notes
- Contact: Yong Cao, Phastar

Visual:

- Clean resource list.
- QR-code space only if a real URL is provided.

Chinese notes:

- Short close.
- Transition to Q&A.

---

## 8. Optional Hidden Appendix

If the tool supports hidden appendix slides, add these backup slides.

### Appendix A: Validation And Regulated Workflows

Visible:

- AI output is a draft.
- Existing review and validation still apply.
- Approval controls side effects.
- Approval does not replace validation.

Chinese notes:

- Explain that this workflow can fit existing review practices, but does not remove them.

### Appendix B: Hallucination Risk

Visible:

- Model proposes.
- Tools provide grounded data.
- Code enforces boundaries.
- Humans review outputs.

Chinese notes:

- Grounding reduces risk, but review remains mandatory.

### Appendix C: Offline Or Restricted Environments

Visible:

- Terminal UI can run locally.
- Model deployment depends on environment.
- Do not upload local files unless policy allows it.

Chinese notes:

- Separate local app architecture from model hosting policy.

### Appendix D: Cost And Latency

Visible:

- Streaming improves perceived latency.
- Tools reduce unnecessary context.
- Smaller models can handle simple steps.

Chinese notes:

- Cost can be controlled by workflow design, model choice, and context discipline.

---

## 9. Source Footnotes

Use small, quiet footnotes only on slides with factual claims about external tools.

Suggested sources:

- Ink: `https://github.com/vadimdemedes/ink`
- AI SDK docs: `https://ai-sdk.dev/docs`
- AI SDK Core: `https://ai-sdk.dev/docs/ai-sdk-core`
- AI SDK UI: `https://ai-sdk.dev/docs/ai-sdk-ui`
- AI SDK tools: `https://ai-sdk.dev/docs/foundations/tools`

Do not clutter slides with long citations.

If the tool can browse current docs, verify current API names before finalizing. If it cannot browse, use the API names as given in this prompt and avoid making more specific claims than necessary.

---

## 10. Quality Bar

Before finalizing, run a contact-sheet review:

- At thumbnail size, the deck shows a coherent visual system and varied slide rhythm.
- Every slide has one clear claim.
- Code is readable and not cramped.
- Demo slides feel like real software, not generic mockups.
- Animation clarifies mechanisms.
- English slide text is concise and grammatically correct.
- Chinese notes are natural and presentation-ready.
- No placeholders, fake links, fake QR codes, or generic AI imagery.

---

## 11. Deliverables

Produce:

1. Editable PowerPoint deck (`.pptx`).
2. Rendered PDF or PNG contact sheet if the tool supports it.
3. A short build note listing:
   - final slide count,
   - whether demo visuals are real captures or mockups,
   - whether hidden appendix slides were included,
   - any missing URLs the speaker must fill in.

The deck is successful when a SAS/statistical programming audience can follow the React, Ink, AI SDK, tools, streaming, and approval story without prior frontend experience.
