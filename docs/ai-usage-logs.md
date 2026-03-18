# AI Usage Log

This log documents every AI interaction made during the development of the
AI-Assisted Full-Stack Developer Induction page. Each entry records the prompt,
what was suggested, what was accepted or rejected, and the reasoning.

---

## Entry 001 — Initial page generation

**Date:** 2025-03-18  
**Tool:** Claude (claude.ai)  
**Branch:** `main` (initial build)

**Prompt:**
> Full prompt provided two PDF source documents (AI_FullStack_Induction_v2.pdf
> and Graded_Debugging_Challenge_v2.pdf) along with a detailed specification
> covering: 12 page sections, video placeholder requirements, resource card
> requirements, interactivity requirements (expand/collapse, copy-to-clipboard,
> smooth scrolling), style guidelines (developer-doc aesthetic, monospace for
> code, card-based layout), and five target intern skillsets to cover.

**AI suggested:**
- Single self-contained HTML file with embedded CSS and vanilla JavaScript
- Dark-mode-first design using CSS custom properties for all colour tokens
- Sticky nav with `IntersectionObserver` for active link highlighting
- Expand/collapse stepper for the 7-step learning workflow
- Tabbed prompt library with copy-to-clipboard on each prompt
- Interactive checklist with live progress bar
- Inline SVG-style system diagram (Frontend → API → Service → Database)
- Code examples drawn directly from the source PDFs (broken code from the
  Debugging Challenge used in the PR Review Simulation module)

**Accepted:** Full output accepted as the initial build. All code examples
verified against the source PDFs to confirm they matched the originals.

**Rejected / Modified:** None at this stage.

**Verified by:** Manual review of all 11 modules in browser; confirmed code
examples match source documents exactly.

---

## Entry 002 — Light/dark theme toggle

**Date:** 2025-03-18  
**Tool:** Claude (claude.ai)  
**Branch:** `feat/light-mode-toggle`

**Prompt:**
> "The current design is dark mode. Can I have the option to enable the light
> mode? Will that work in a static page?"

**AI suggested:**
- `html[data-theme="light"]` CSS block redefining all custom properties
- Toggle button in the nav bar with sun/moon icon
- `localStorage` persistence so the preference survives page reloads
- Self-invoking function on page load to apply saved theme before paint,
  preventing flash-of-incorrect-theme
- Fixing several hardcoded hex values (`#0d1520`, `#e8f0fc`) that would not
  respond to the variable override

**Accepted:** Full implementation accepted. Confirmed `localStorage` works
correctly in static GitHub Pages environments (it is a browser API, not
server-side).

**Rejected / Modified:** None.

**Verified by:** Toggled between modes in browser; confirmed preference
persists across page reload; confirmed all components (code blocks, video
cards, prompt boxes, do/don't cards) update correctly in both modes.

---

## Entry 003 — GitHub repo scaffold

**Date:** 2025-03-18  
**Tool:** Claude (claude.ai)  
**Branch:** `main` (new repo setup)

**Prompt:**
> "I need to create a Github repo for this code which will have:
> 1. README that explains the structure
> 2. Have a wiki with pages for UI/UX design, Pedagogic Design, Examples used,
>    Mini Project idea
> 3. Github Workflow that enables auto update of the page whenever a new change
>    is merged
> 4. Feedback template (similar to https://github.com/jkmpod/code-to-cloud)"

**AI suggested:**
- `README.md` covering repo structure, live URL, content module table,
  local dev instructions, and wiki sync instructions
- `.github/workflows/pages.yml` using `actions/upload-pages-artifact` and
  `actions/deploy-pages` with a startup check that fails if `index.html`
  is missing
- `.github/ISSUE_TEMPLATE/feedback.yml` — structured form with dropdowns for
  role, module, difficulty, AI guidance usefulness, and an overall star rating
- `.github/ISSUE_TEMPLATE/content_suggestion.yml` — form for suggesting new
  resources or examples
- `wiki/` directory with five pages: Home, UI-UX-Design, Pedagogic-Design,
  Examples-Used, Mini-Project-Idea
- Pedagogic Design wiki page referencing Sweller (1988), Reigeluth (1999),
  Beck (2002), and Fowler (2018) as theoretical grounding

**Accepted:** Full output accepted.

**Rejected / Modified:** None. All wiki internal links manually updated from
`YOUR_USERNAME/YOUR_REPO` placeholders to `jkmpod/code-to-cloud` before
committing.

**Verified by:** Reviewed all five wiki pages for accuracy; confirmed the
GitHub Actions workflow syntax against GitHub's official documentation.

---

## Entry 004 — Integration into existing repo

**Date:** 2025-03-18  
**Tool:** Claude (claude.ai)  
**Branch:** `feat/add-induction-page`

**Prompt:**
> "Can this be appended to the existing github repo
> https://github.com/jkmpod/code-to-cloud, and still retain the ease of
> rendering it through github.io?"

**AI suggested:**
- Place the induction page at `induction/index.html` — GitHub Pages serves
  `index.html` from any subdirectory automatically, no workflow changes needed
- Resulting URLs: root stays at `/code-to-cloud/`, induction at
  `/code-to-cloud/induction/`
- Add a `← code-to-cloud` back-link in the induction nav bar
- Append an induction section to the existing `README.md` rather than
  replacing it
- All wiki files and issue templates already use real `jkmpod/code-to-cloud`
  links after the prior step

**AI also noted:** The existing `deploy.yml` uploads the entire repo root,
so GitHub Pages already serves subdirectories — no workflow modification
required.

**Accepted:** Full approach accepted. Confirmed by checking the live site
structure at `https://jkmpod.github.io/code-to-cloud`.

**Rejected / Modified:** None.

**Verified by:** Fetched the existing live site to confirm the workflow
behaviour before accepting the no-workflow-change conclusion.

---

## Entry 005 — GitHub icon in header and footer

**Date:** 2025-03-18  
**Tool:** Claude (claude.ai)  
**Branch:** `feat/github-icon-nav-footer`

**Prompt:**
> "I need to have a github icon in my header and footer so that interested
> viewers can visit the repo. What changes should I make?"

**AI suggested:**
- Inline SVG of the GitHub mark (from GitHub's Primer design system) rather
  than an image file or emoji
- Placement: immediately after the theme toggle button in the nav; as a
  styled anchor in the footer
- `currentColor` fill so the icon inherits the surrounding text colour and
  responds to hover state and theme changes without extra CSS
- `rel="noopener noreferrer"` on both links (security best practice for
  `target="_blank"`)

**AI reasoning for inline SVG over alternatives:**
- No external image request — page stays fully self-contained
- Scales perfectly on retina displays
- Automatically adapts to dark and light themes via `currentColor`
- GitHub logo is trademarked — using the official Primer SVG path is
  the correct approach

**Accepted:** Full suggestion accepted.

**Rejected / Modified:** None.

**Verified by:** Changes were provided as instructions rather than applied
directly — to be verified after manual implementation in the file.

---

## Entry 006 — Template tree formatting fix

**Date:** 2025-03-18  
**Tool:** Claude (claude.ai)  
**Branch:** `fix/template-tree-formatting`

**Prompt:**
> Shared a screenshot of Module 04 showing the directory tree structure
> collapsed into a single unreadable block of text. Asked what change
> needs to be made to fix the formatting issue.

**AI identified root cause:**
The template tree was wrapped in a `<div>` instead of a `<pre>` tag.
A `<div>` collapses all whitespace — newlines, spaces, and indentation —
into a single flow. The tree characters (`├──`, `│`, `└──`) were present
but rendered on one line because the line breaks were stripped.

**AI suggested:**
1. Change `<div class="template-tree">` to `<pre class="template-tree">`
   and the closing tag accordingly
2. Add `white-space: pre` to the `.template-tree` CSS rule to explicitly
   preserve whitespace
3. Add `overflow-x: auto` to prevent horizontal overflow on small screens
4. Noted the global `pre` style conflict (padding and border already
   defined globally) — the `.template-tree` class values take precedence
   via specificity, so no additional override needed

**Accepted:** Full diagnosis and fix accepted.

**Rejected / Modified:** None.

**Verified by:** To be confirmed after applying the change locally and
viewing Module 04 in both dark and light modes before committing.

---

## Log format reference

Each entry must include:

| Field | Description |
|-------|-------------|
| Date | Month and year of the interaction |
| Tool | AI tool used |
| Branch | Git branch the change was made on |
| Prompt | Exact or close paraphrase of what was asked |
| AI suggested | What the AI recommended |
| Accepted | What was used without modification |
| Rejected / Modified | What was changed or not used, and why |
| Verified by | How the output was checked before committing |