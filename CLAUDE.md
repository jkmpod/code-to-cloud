# CLAUDE.md

This file is intended for contributors using an agentic AI (Claude, Copilot, Cursor, etc.) to help develop content for this tutorial. It encodes the design and pedagogical decisions that must be preserved in any new chapter or modification.

Read this file fully before generating or editing any content in `index.html`.

---

## What this project is

**Code to Cloud** is an interactive, scrollytelling tutorial for novice developers who have never deployed an application. It covers the journey from local code to a live GCP deployment across eight chapters.

The audience is **not** an experienced developer looking for a reference. It is someone who can write code but has never used Git properly, never built a Docker container, and has no mental model of how cloud infrastructure works.

Every content decision — what to include, how to explain it, which element to use — should be evaluated against that audience.

---

## Before you generate a new chapter

Ask and answer these questions before writing any HTML:

1. **Does this concept belong in the sequence?** Chapters follow the real-world order a developer encounters these concepts when deploying for the first time. A new chapter must fit logically between existing ones, not just be appended.

2. **What does the learner already know by this point?** Build on prior chapters. Do not re-explain concepts already covered.

3. **What is the single most important thing the learner must leave this chapter knowing?** Write the `<p class="lede">` first. If you cannot summarise the chapter in two sentences for a novice, the scope is too broad.

4. **What is the most common mistake a novice makes with this concept?** That mistake becomes a `<div class="callout cd">` (danger callout) placed at the moment of highest risk — not at the start, not at the end.

5. **What analogy bridges this concept to something the learner already understands?** That analogy goes in the concept table. If you cannot find a concrete analogy, the concept may not be ready to teach yet.

---

## Pedagogical rules — do not break these

### Rule 1: Every new concept needs an analogy before a definition

Every chapter opens with a concept table (`<table class="ctable">`) that maps new vocabulary to familiar ideas. The format is always:

| New term | Think of it as… | What it actually does |

Do not skip the analogy column. Do not use another technical term as the analogy. The analogy must be non-technical.

This is grounded in Ausubel's assimilation theory — new knowledge is retained only when anchored to existing cognitive structures.

### Rule 2: Show worked examples, not abstract descriptions

Every concept must be demonstrated with a concrete, runnable example — a terminal session, a YAML file, a Dockerfile. The terminal block format is:

```html
<div class="term">
  <div class="tbar">
    <div class="td r"></div><div class="td y"></div><div class="td g"></div>
    <div class="tname">bash</div>
  </div>
  <div class="tbody">
    <div><span class="tc"># comment explaining what this does</span></div>
    <div><span class="tp">$ </span><span class="tcmd">actual command here</span></div>
    <div><span class="tok">✓ Expected output</span></div>
  </div>
</div>
```

Terminal span classes: `.tc` comment · `.tp` prompt · `.tcmd` command · `.tv` variable/value · `.tok` success output · `.to` neutral output · `.tw` warning output

Commands must be real and runnable. Do not invent flags or options. Do not use placeholder commands like `<your-command-here>` — use realistic values instead.

### Rule 3: Multi-step workflows use wizards, not lists

If a concept involves more than two sequential steps, use the step wizard pattern, not a numbered list. A novice who sees ten steps at once will skim; a wizard forces one step at a time.

Wizard structure:

```html
<div class="wiz">
  <div class="wsteps">
    <button class="wsb active" onclick="wiz('KEY',0)"><span class="wsn">1</span>Step Name</button>
    <button class="wsb" onclick="wiz('KEY',1)"><span class="wsn">2</span>Step Name</button>
  </div>
  <div id="KEY-0" class="wp active">...</div>
  <div id="KEY-1" class="wp">...</div>
</div>
```

The `KEY` must be unique across the entire file. Check existing keys before adding: `g` (Git), `d` (Docker), `dc` (Docker Compose), `lnt` (Linting).

### Rule 4: Error prevention over error correction

Identify the one or two mistakes a novice is most likely to make in this chapter. Surface them as danger callouts (`<div class="callout cd">`) at the exact point in the content where the mistake would occur — not in a summary at the end.

The callout title should be a specific prohibition, not a general warning. Good: `🚫 Never commit directly to main`. Bad: `⚠️ Be careful with Git`.

### Rule 5: Every chapter must have all three modalities

A complete chapter always includes:
- Written explanation (concept table + prose + callouts)
- A worked example (terminal block, code block, or YAML)
- An embedded YouTube video + resource links at the bottom

The video and resources section structure:

```html
<div class="vid-section">
  <div class="vid-label">Watch: [Descriptive title]</div>
  <div class="vid-wrap">
    <iframe src="https://www.youtube.com/embed/VIDEO_ID" allowfullscreen loading="lazy"></iframe>
  </div>
</div>
<div class="res-section">
  <div class="res-label">📚 Additional Resources</div>
  <div class="res-links">
    <a class="res-link" href="URL" target="_blank" rel="noopener">Link Label</a>
  </div>
</div>
```

Only use real, verified YouTube video IDs. Do not hallucinate video IDs. If you are unsure of a video ID, leave a `<!-- TODO: verify video ID -->` comment rather than inserting a guess.

---

## Design rules — do not break these

### Fonts

Do not introduce new font families. The three fonts in use are locked:
- `var(--serif)` — `Fraunces` — headings only (`h1`, `h2`)
- `var(--sans)` — `Plus Jakarta Sans` — all body copy
- `var(--mono)` — `JetBrains Mono` — all code, labels, metadata

### Colours

Do not add new colour variables. Use only what is defined in `:root`:

| Variable | Value | When to use |
|----------|-------|-------------|
| `--accent` / `--accent-l` | GCP blue | Primary interactive elements, tags, links |
| `--green` / `--green-l` | Success green | `.cs` callouts, success states, `.tg` tags |
| `--amber` / `--amber-l` | Warning amber | `.cw` callouts, `.ta` tags |
| `--red` / `--red-l` | Danger red | `.cd` callouts, `.tr` tags |
| `--ink`, `--ink-2`, `--ink-3` | Ink scale | Body text hierarchy |
| `--rule`, `--rule-2`, `--bg` | Surface scale | Borders, backgrounds |

Do not use colour for decoration. Every colour use must carry semantic meaning.

### Section structure

Every chapter section follows this exact structure:

```html
<section id="sN">
<div class="inner">
  <div class="ch-label"><span class="ch-num">0N</span><span class="ch-rule"></span></div>
  <h2>[Heading with optional <em>italic accent</em>]</h2>
  <p class="lede">[Two-sentence summary for a novice]</p>

  <!-- content elements -->

  <div class="vid-section">...</div>
  <div class="res-section">...</div>
</div>
</section>
```

The `id` must follow the pattern: `s1`, `s2`, `s3`... or `s4b` for sub-chapters. The chapter number in `.ch-num` must match.

The `<h2>` heading should use a line break (`<br>`) to control where the italic accent word falls. The italic (`<em>`) is always the most conceptually important word or phrase in the heading.

### Callout types and when to use each

| Class | Colour | Use for |
|-------|--------|---------|
| `.ci` | Blue | Neutral information, definitions, tips |
| `.cw` | Amber | Cautions — things that might cause problems |
| `.cd` | Red | Prohibitions — things that will cause serious problems |
| `.cs` | Green | Recommendations, confirmations, good patterns |

Use at most two callouts per chapter. More than two signals the chapter scope is too wide.

### Nav button

Every new chapter needs a nav button added inside `<nav>` in the correct sequence position:

```html
<button class="nav-ch" onclick="jump('sN')">0N Label</button>
```

Keep labels short — two or three words maximum. The nav overflows and hides on small screens; verbose labels break the layout.

---

## What not to generate

- **Do not add inline styles** — use existing CSS classes. If a class does not exist for what you need, question whether the design needs it at all.
- **Do not add new JavaScript functions** — the existing `wiz()`, `chk()`, and scroll observer cover all interactive patterns. New interactions require a design discussion first.
- **Do not add new font imports** — the three fonts are final.
- **Do not add dark mode, animations, or new colour schemes** — these are out of scope.
- **Do not write comprehensive reference content** — this is a first mental model. If the content reads like documentation, it is too detailed. Link to the official docs instead.
- **Do not add checklist items for tools not covered in a chapter** — every item in Chapter 08 must map to a concept taught somewhere in the tutorial. If a tool appears in the checklist but has no chapter, add the chapter first.
- **Do not invent terminal output** — every `<span class="tok">` or `<span class="to">` line must reflect what the real command actually outputs.

---

## Checklist before submitting generated content

Before proposing any generated chapter or edit, verify:

- [ ] The chapter has a concept table with non-technical analogies
- [ ] Multi-step workflows use the wizard pattern, not a list
- [ ] The most common novice mistake is a `cd` danger callout at the point of risk
- [ ] All terminal commands are real and runnable
- [ ] A YouTube video is embedded (with a verified, real video ID)
- [ ] At least two external resource links are included
- [ ] No new fonts, colours, or JavaScript functions were introduced
- [ ] The nav button has been added in the correct sequence position
- [ ] The `README.md` What's covered table has been updated
- [ ] The section `id` and chapter number are consistent
- [ ] Any new concept that has a lint check implication has a corresponding item added to the Chapter 08 pre-deploy checklist

---

## Reference

- [Design Philosophy](../../wiki/Design-Philosophy) — full rationale for visual and structural decisions
- [Pedagogy](../../wiki/Pedagogy) — full rationale for teaching and learning decisions
- [CONTRIBUTING.md](CONTRIBUTING.md) — branch naming, commit format, PR process