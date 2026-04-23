---
name: Design Process
description: >
  A disciplined process for producing design artifacts (websites, prototypes,
  slides, covers, mobile screens) with the user acting as a design manager and
  Claude acting as a senior designer. Optimizes for clarity of intent,
  breadth of exploration, and iteration speed — not for first-shot perfection.
when_to_use: >
  Any time the user asks for a visual artifact in HTML — landing pages, personal
  sites, portfolios, slide decks, social assets, mobile mockups, animations,
  prototypes. Skip for trivial edits ("change the color to red") and for
  purely engineering tasks.
applies_to: Claude Projects, Claude.ai conversations, Claude Code / Cursor
language: en
---

# Design Process — A Skill for Building Visual Artifacts with Claude

This skill describes **how** to work, not **what** to build. It is the process
I (Claude) follow when the user gives me a design brief. It applies to any
visual artifact: a personal site, a slide deck, a social cover, a mobile
prototype, an animated video.

The process has five phases:

1. **Intake** — ask until the ambiguity is gone.
2. **Context** — read everything relevant before drawing a pixel.
3. **Proposal** — state assumptions + system before building.
4. **Build** — one file, many variations, expose decisions as tweaks.
5. **Iterate** — respond to feedback honestly, fold variants back in.

Each phase has entry criteria, exit criteria, and anti-patterns. **Skipping a
phase is the most common way this process fails.**

---

## Phase 1 — Intake

### Goal
Replace the user's implicit model of the output with an explicit one — written
down, visible to both sides, checkable later.

### Entry criterion
The user has asked for something, and at least one of the following is true:
- The ask is vague ("make me a portfolio").
- The output format has multiple valid interpretations ("a deck on X").
- You do not yet know the brand, design system, or prior art to build from.
- The ask implies variants but no axes ("give me options for the hero").

If none are true — e.g. the user said "change the accent to `#6D3FD9`" —
**skip Intake**. Ambiguity checks that aren't needed burn trust.

### What to do
Ask **at least 10** focused questions in a single batch. Use a structured
question tool if the environment has one; otherwise use a numbered list. Do
not ask questions one at a time — it is slow and makes the user feel
interrogated.

### The question taxonomy

Every design brief benefits from questions across these axes. Pick the ones
that matter for the specific ask, but cover each axis at least once.

1. **Starting point / context.**
   - Do you have an existing design system, UI kit, brand, or codebase I should
     match?
   - Screenshots of prior work? A Figma file? A competitor you like?
   - If none — do you want me to set an aesthetic direction, or do you want
     to define one first?

2. **Audience.**
   - Who is this for? (recruiters, peers, conference attendees, customers)
   - What should they do or feel after seeing it?
   - What do they already know about you / the product?

3. **Format & fidelity.**
   - Hi-fi pixel-perfect, hand-drawn wireframe, or somewhere between?
   - Static images, interactive prototype, or production code?
   - Fixed aspect ratio (deck, social cover), responsive (site), or device-bound
     (mobile)?

4. **Variations — the single most important question set.**
   - How many directions of the **overall system** do you want? (1 / 3 / 6+)
   - Which specific elements should get variations? (hero, nav, color, type,
     layout, copy, imagery)
   - How divergent should variations be? (all safe / mix safe and novel /
     push the form)
   - What do you want the variations to **explore**? (visual style /
     interaction pattern / information hierarchy / emotional tone /
     technical approach)

5. **Constraints.**
   - Accessibility targets? (contrast, touch, keyboard)
   - Dark / light / both?
   - Bilingual? Which languages, and should layouts differ per language?
   - Anything you explicitly do **not** want?

6. **Content.**
   - Is copy final or placeholder?
   - Do you have real images/assets, or should I use placeholders?
   - If placeholders — what level of polish? (grey boxes / rough SVGs /
     realistic stock)

7. **Tweaks & editability.**
   - Which decisions do you want to be able to change yourself later?
     (colors, fonts, copy, layout variants, feature flags)
   - Do you want a single file where variants toggle, or separate files per
     variant?

8. **Success criteria.**
   - How will you know this is done?
   - What's the one thing you'd be upset about if I got wrong?

### Offer escape hatches
Every multiple-choice question should include:
- "Explore a few options" — user delegates the axis.
- "Decide for me" — user explicitly transfers authority.
- "Other (specify)" — freeform for anything you didn't anticipate.

### Exit criterion
You can write a one-paragraph brief that covers: audience, format, aesthetic
direction, number and axes of variations, constraints, tweaks. If you cannot,
ask another round.

### Anti-patterns
- **Over-asking on small tasks.** If the user said "change the hero copy to X,"
  just do it. Questions are friction — use them when they save more time than
  they cost.
- **Asking then ignoring.** If the user said "use Space Grotesk," do not ask
  about font choice again two turns later.
- **Yes/no questions that aren't really yes/no.** "Do you want variations?" is
  worse than "How many variations — 1, 3, or 6+?"
- **Asking about implementation before asking about intent.** Do not ask
  "React or plain HTML?" before you know what's being built.

---

## Phase 2 — Context

### Goal
Understand the visual, verbal, and structural language of what already exists,
so that what you add belongs to it.

### Entry criterion
The user has given you a starting point: a codebase, a design system, a UI kit,
screenshots, a brand document, an existing site. Or has confirmed there is
none, and you are starting from zero.

### What to do

**If context exists:**
1. List all relevant files / assets. Read them all, not just the ones that look
   important.
2. Extract the **tokens**: colors (hex codes, not names), type scale (exact
   sizes, weights, line-heights), spacing scale, border-radii, shadows,
   motion (timing, easing).
3. Extract the **vocabulary**: how are buttons named? What's the copy tone?
   Are sentences terminal or fragment-style? Does the brand use emoji / icons
   / neither?
4. Extract the **system rules**: when is a divider a 1px line vs 2px?
   When does a card get a shadow vs a border? What's the hover convention?
5. Write your findings down before drawing. This forces you to actually see
   the system instead of eyeballing it.

**If no context exists:**
1. Invoke the Frontend Design skill (or equivalent) to commit to a specific
   aesthetic direction. "Modern and clean" is not a direction. "Editorial
   magazine with warm neutrals and a serif display face" is.
2. Pick actual type faces, actual hex codes, an actual spacing unit.
3. Name the direction — you'll reference it later when the user asks "can we
   try another direction?"

### Exit criterion
You can write a paragraph that describes the design system in enough detail
that a different designer could build a new screen in it without seeing the
existing screens.

### Anti-patterns
- **Approximating from memory.** If the repo has a `theme.ts`, read it. Do
  not infer colors from a screenshot.
- **Copy-pasting without reading.** If you import a component, understand its
  props, states, and intended uses before placing it.
- **Stopping at one source.** A project may have multiple design systems — a
  UI kit for app screens, a marketing system for the landing page. Find them
  all.
- **Generating a logo / hero image / icon you don't have.** Use a placeholder
  and flag it. Fake confidence with an AI-generated SVG is worse than an
  honest grey box.

---

## Phase 3 — Proposal

### Goal
Before writing the final artifact, state what you're about to do — in writing,
in the artifact itself — so the user can correct you cheaply.

### Entry criterion
Intake and Context are complete. You have a brief and a system.

### What to do
Open a draft file and write **three things**, in order:

1. **Assumptions.** One bulleted list. "I'm assuming the audience is hiring
   managers, the brand is established, copy is placeholder, we want 3 hero
   variations differing in layout and density, tweaks for accent color and
   spacing scale." If any bullet is wrong, the user will tell you now — not
   after you've built the wrong thing.

2. **The system.** What you'll use for type, color, spacing, rhythm, imagery
   strategy. Commit to it. "Space Grotesk for display, Inter for body, two
   background colors max (ink + paper), one accent token swappable via
   tweaks." This is your rubric for every subsequent decision.

3. **Placeholders for each piece.** A file skeleton with empty sections
   labeled by what will go in them. Not implementation — just the outline.
   `<!-- Hero: variation A (large type + photo) -->`,
   `<!-- Projects grid: 2-up cards -->`, etc.

Show this to the user **before building**. They will either approve or
redirect — cheaper than rework after rendering.

### Exit criterion
The user has seen the proposal. You have explicit approval or explicit changes.
Never build past Proposal without this.

### Anti-patterns
- **Silent assumptions.** If you assumed something, name it. Users cannot
  correct thoughts they can't see.
- **Starting from a blank canvas.** You're not a junior grinding pixels — you
  are a senior articulating a plan. Skipping the plan to "get something on
  screen faster" produces work that has to be thrown away.
- **Committing to zero variants in the proposal.** If the brief asks for
  options, the proposal must enumerate which options and on which axes.

---

## Phase 4 — Build

### Goal
Produce the artifact, with variations exposed as toggles inside a single file,
with decisions parameterized as tweaks.

### Core principles

#### 4.1 One file, many variations
Do not produce `hero-v1.html`, `hero-v2.html`, `hero-v3.html`. Produce
`hero.html` with a visible toggle (tab bar, segmented control, keyboard
shortcut, or tweak panel) that switches between variations.

Why: users need to **compare** variants, not hunt for them. They need to mix
(take the layout from A and the color from C). Separate files prevent mixing.

**Exception:** if variations differ fundamentally in content or IA — e.g. a
resume vs a portfolio vs a blog — separate files are correct.

#### 4.2 Give at least 3 variations on any axis the user asked to explore
Three is the minimum because two is a binary (safe vs bold) and the user
usually needs the third to break the binary. Mix registers:
- **Variant A — By-the-book.** Uses the existing system faithfully. Safe.
- **Variant B — Elevated.** Same system, pushed harder: bigger type, more
  whitespace, a gesture the system allows but rarely uses.
- **Variant C — Divergent.** Breaks a rule deliberately in service of the
  idea. Different layout logic, different metaphor, or a new visual device.

If the user asked for 6+: A, B, C, then three more that explore different
**axes entirely** (a wildly different color treatment, a typographic
blowout, a motion-first take).

#### 4.3 Tweaks as a first-class surface
Any decision the user might second-guess should be exposed as a tweak —
a visible control inside the artifact that changes the decision live.

Minimum tweak set for most design projects:
- **Accent color** (2–4 named palettes, not a color picker).
- **Wordmark / primary text** (if brand identity is in flux).
- **Density / scale** (compact / default / roomy).
- **Variant switcher** (A / B / C for any explored axis).

Persist tweak state so the user can refresh without losing it (localStorage
is fine). Label the panel "Tweaks" to match convention. Hide the panel when
tweaks mode is off — the design should look final without the controls.

#### 4.4 Persistent state
Any stateful UI (current slide, current tab, scroll position, tweak values)
must survive reload. Store in localStorage, re-read on mount. This is
non-negotiable — users refresh constantly while iterating.

#### 4.5 Typography is not negotiable
- **Slides (1920×1080):** body text ≥ 24px, headlines ≥ 72px.
- **Print documents:** body ≥ 12pt.
- **Mobile:** hit targets ≥ 44×44px. Body text ≥ 15px.
- **Never use:** Inter (overused), Roboto, Arial, system-ui as the primary
  display face. These are defaults — defaults are anti-design.
- **Prefer:** commit to a specific face with character. Space Grotesk,
  Söhne, GT America, IBM Plex, Fraktion, Neue Haas Grotesk, Tiempos,
  Söhne Mono, JetBrains Mono. If the brand has its own, use that.

#### 4.6 Color is not negotiable
- If the brand has colors, use those. Period.
- If not, pick **one** accent. Derive shades with OKLCH, not by eyeballing
  HSL. Keep the neutral palette restrained (≤ 5 grays).
- **Avoid:** gratuitous gradients, "glassmorphism" for its own sake,
  rainbow chip rows, every-section-a-different-background.

#### 4.7 Content discipline
- **Never fill empty space with filler.** If a section feels empty, that's a
  layout problem, not a content problem. Do not invent testimonials,
  statistics, FAQ entries, or team members.
- **Ask before adding sections.** If you think the page needs a "Pricing"
  block, ask the user — they know whether pricing is relevant.
- **Avoid data slop.** Fake numbers, fake logos, fake icon grids with six
  identical-looking items. Less is more.

#### 4.8 The AI-slop blocklist
These tropes mark work as lazy. Avoid reflexively:
- Gradient-washed hero backgrounds as the main visual interest.
- Emoji in UI chrome (buttons, nav, labels) unless the brand uses them.
- `border-left: 4px solid {accent}` "callout" cards.
- Auto-generated hero SVGs (blobs, waves, gradient orbs).
- "Modern minimal" as an aesthetic — commit to a specific adjective instead.
- Inter + rounded corners + gray-50 background. This is the 2024 default.
- Six-card grids where every card has an identical rounded icon.

When tempted to use any of these, ask: "Is this carrying meaning, or filling
space?" If filling space, remove.

### Exit criterion
The file renders without errors, all variations are reachable, all tweaks
work, state persists. You have **not** verified visual correctness yourself
yet — that's the next phase's job.

### Anti-patterns
- **Shipping N separate files for variants.** Hurts comparability.
- **Variants that differ only trivially.** Three hero colors on the same
  layout is not three variants — it's one variant with a color tweak.
- **Adding features the user didn't ask for** ("I also added a testimonials
  section"). Ask first.
- **Over-animating.** If it moves, it should carry meaning. Decorative
  motion is AI slop with a timeline.

---

## Phase 5 — Iterate

### Goal
Fold feedback in without losing prior work or ballooning file count.

### What to do

1. **Surface the artifact immediately.** Open it in the user's view the
   moment it renders cleanly, before you feel "done." Users iterate on what
   they can see, not on what you're planning.

2. **Verify cleanly.** Check for console errors, broken states, missing
   assets. If something is broken, fix it before asking for feedback —
   don't make the user debug for you.

3. **Fold new variants in, don't fork.** When the user says "can we try
   another direction with more editorial feel?" — add a new variant to the
   existing file, not a new file. Exception: fundamental IA shift.

4. **Respond to feedback honestly.** If the user says "the amber looks like
   a porn site" — engage with the observation, don't deflect. Give them
   your actual read: "You're right, black + heavy amber pulls that
   association. Swap the accent to violet and it dissolves." Honest beats
   polite.

5. **When the user provides a constraint, propagate it.** If they say
   "actually the domain is `example.com`" — find every place the old domain
   appears (site footer, slides, social covers, portfolio, i18n strings)
   and update them all. Half-propagated changes create ghost states.

6. **Summarize at the end of each turn.** One sentence per change. Not a
   wall of text. Users scan summaries; they don't read them.

### Exit criterion per turn
The user can see the change, can compare it to what came before (via tweak
toggle or side-by-side), and knows exactly what you did.

### Anti-patterns
- **Silent regressions.** You fix one thing and break another. Run a quick
  sanity check before calling it done.
- **"I also cleaned up…"** Don't make changes the user didn't ask for.
  They'll spot the unwanted change and lose trust in the explicit ones.
- **Defensive over-explanation.** The user doesn't need you to justify
  every pixel. Summaries are brief.
- **Hiding uncertainty.** If you're not sure a change is right, say so and
  offer the alternative. "I shifted the headline size up; if it feels too
  heavy, the tweak for type-scale is now 0.9 — toggle and compare."

---

## Patterns & templates

### Intake question template (slot-filled for any project)

```
Quick questions about {thing}:

1. Starting point: do you have an existing {design system / brand / codebase / screenshots} I should match, or am I setting direction?
2. Audience: who is this for, and what should they do after seeing it?
3. Format: {fidelity options — wireframe / hi-fi / prototype / production}?
4. Variations: how many directions of the overall {thing}? (1 / 3 / 6+)
5. Variation axes: which elements get variants — layout, color, type, copy, imagery, interaction?
6. Divergence: all safe and on-brand, mixed, or push the form?
7. Constraints: dark/light, bilingual, accessibility, anything you explicitly don't want?
8. Content: is copy final? Real assets or placeholders?
9. Tweaks: which decisions should you be able to change live — colors, fonts, copy, variants?
10. Success: how will you know this is done? What would upset you if I got it wrong?
```

### Proposal template (top of a draft file)

```html
<!--
  {Project name}
  ─────────────────────────────────────────────────

  ASSUMPTIONS (correct me if wrong):
  - Audience: {...}
  - Format: {...}
  - Tone: {...}
  - Variations: {N} directions, exploring {axes}
  - Placeholders: {what's real, what's fake}

  SYSTEM:
  - Type: {display face} + {body face}
  - Colors: {ink} / {paper} / {accent + swaps}
  - Spacing unit: {N}px, scale {1, 2, 3, 5, 8}
  - Imagery: {approach}
  - Density: {compact / default / roomy}

  PLACEHOLDERS:
  [ ] Hero (3 variants: A safe, B elevated, C divergent)
  [ ] Section 2 ...
  [ ] Footer ...
-->
```

### Tweak panel skeleton (protocol)

```js
// 1. Register listener BEFORE announcing availability
window.addEventListener('message', (e) => {
  if (e.data?.type === '__activate_edit_mode') showPanel();
  if (e.data?.type === '__deactivate_edit_mode') hidePanel();
});

// 2. Then announce
window.parent.postMessage({ type: '__edit_mode_available' }, '*');

// 3. Persist changes
function commit(edits) {
  window.parent.postMessage({ type: '__edit_mode_set_keys', edits }, '*');
}

// 4. Wrap defaults in magic comments so the host can persist them
const TWEAK_DEFAULTS = /*EDITMODE-BEGIN*/{
  "accent": "royal",
  "density": "default",
  "heroVariant": "A"
}/*EDITMODE-END*/;
```

### Accent swap pattern (for CSS variable systems)

```css
:root { --accent-c: #6D3FD9; --accent-dk: #4F22B5; }
:root[data-accent="amber"]  { --accent-c: #E8A54B; --accent-dk: #B8791F; }
:root[data-accent="royal"]  { --accent-c: #6D3FD9; --accent-dk: #4F22B5; }
:root[data-accent="indigo"] { --accent-c: #5B4BFF; --accent-dk: #3A2BD1; }
:root[data-accent="violet"] { --accent-c: #8B5CF6; --accent-dk: #6D3FD9; }
```

Then every hardcoded accent in components becomes `var(--accent-c)` — a single
tweak cascade changes the entire system.

---

## Telltale signs the process is working

- The user says "actually, can we also try…" and you add a variant in the
  same file in under a minute.
- The user catches an association or connotation you missed, and you engage
  with it rather than deflecting.
- A change to a token (accent, font, spacing) propagates correctly across
  every page / slide / artifact without the user listing where to look.
- The file grows by variants, not by forks.
- Late-stage changes are cheap.

## Telltale signs it's failing

- You're on `design-v4-final-FINAL.html`.
- Three variants look identical except for color.
- The user repeats a constraint they already gave you.
- You added a section / feature / color the user didn't ask for.
- A tweak breaks on reload because state isn't persisted.
- Your summaries are longer than the user's requests.

---

## Minimum viable pass

If you can only do one thing from this skill, do this:

**Before building anything, write down — in the artifact itself — what you
are about to build, why, and what variations you will explore. Show it to
the user. Wait for a response. Then build.**

Everything else in this document is an elaboration of that single rule.
