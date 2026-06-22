---
name: anti-slop-ui
description: >
  Enforce professional, human-centric UI/UX design standards that eliminate AI design anti-patterns.
  ALWAYS use this skill when building, reviewing, or iterating on any frontend UI — including React artifacts, HTML pages, dashboards, forms, landing pages, onboarding flows, and admin panels. Trigger whenever the user asks to "make it look professional", "clean this up", "redesign", "make it not look AI-generated", or when generating any visual component for production use. Use alongside frontend-design for all new UI work. Do not skip this skill for "quick" or "simple" UI tasks — AI design anti-patterns appear most often in supposedly simple outputs.
---

# Anti-Slop UI

This skill enforces a concrete set of design prohibitions and quality gates. It is a constraint layer, not a style guide. Pair it with `frontend-design` for aesthetic direction; use this skill to police the output before it ships.

---

## The Core Problem

AI-generated UI is identifiable. Not because it's ugly — it often looks passable at a glance — but because it relies on a small repertoire of learned patterns applied indiscriminately. The result is interfaces that feel assembled rather than designed: status badges nobody asked for, gradients applied to everything that isn't locked down, hover animations that exist because they were trained into the model, and layouts that look like a Tailwind starter kit.

The goal is not "clean" or "minimal" in the aesthetic sense. The goal is **designed**: every element present because a real decision put it there, not because it was the default output.

---

## Prohibited Patterns

### 1. Unsolicited Status Indicators

**Do not add** badges, chips, pills, tags, or inline labels (`LIVE`, `NEW`, `HOT`, `BETA`, `PRO`, `FEATURED`, `POPULAR`) unless:
- The user explicitly requested them, **or**
- They convey real-time system state the user cannot infer (e.g., a live connection status in a monitoring tool)

If something is new, it's new because it was just added — the date or context communicates that. A badge does not add information; it adds noise.

### 2. Gradient Overuse

**Do not apply gradients** to:
- Body text or display headings
- Button backgrounds (unless the brand explicitly uses them)
- Card borders or container outlines
- Hero backgrounds as a default "polish" move

Gradients are a specific design choice. They require justification. A two-color linear gradient behind a headline is not a design decision; it's a placeholder that learned to look like one.

**Acceptable gradient use**: charts, data visualizations, background textures with intentional art direction, or explicit user request.

### 3. Ambient and Decorative Animation

**Do not add** animations that:
- Loop continuously without user interaction (pulsing dots, floating blobs, breathing glows)
- Trigger on scroll for purely decorative reasons
- Apply entrance animations to every element on a page
- Add hover shimmer or glow effects to static informational elements

**Acceptable animation**: button press states, modal open/close transitions, form validation feedback, skeleton loading states, and page-level transitions that aid orientation.

The test: if the animation were removed, would the user lose any information or feel any friction? If no — remove it.

### 4. Generic Layout Templates

**Do not produce** layouts that match recognizable boilerplate patterns:
- Centered hero with gradient text headline, subheadline, two CTA buttons, and a mock browser frame below
- Three-column "features" section with icon + bold title + two-sentence description repeated identically
- "Trusted by" logo row as a default social proof element
- Pricing cards with a "Most Popular" badge on the middle tier
- Footer with four identical link columns

If the content calls for a three-column feature section, fine — but the structure should emerge from the content, not the other way around. Populate with real copy and let that copy determine the layout.

### 5. Orphaned or Unanchored Elements

**Do not place** UI elements that float outside the grid:
- Decorative blobs or shapes positioned with absolute offsets for "visual interest"
- Floating action buttons with no spatial relationship to their context
- Cards with inconsistent margin/padding that breaks grid alignment

Every element belongs to a containing system. If it doesn't, remove it.

---

## Pre-Output Quality Gate

Run this checklist mentally before writing any UI code. If you cannot answer yes to all five, revise before proceeding.

1. **No unsolicited badges** — Is every status indicator or label present because the content requires it?
2. **Gradient discipline** — Is every gradient a deliberate design choice, not a default polish move?
3. **Animation necessity** — Does every animation communicate something, or does it just move?
4. **Layout originality** — Does this layout derive from the content, or does the content fill a pre-existing mold?
5. **Tacky check** — Would a senior product designer at a company like Linear, Vercel, or Stripe look at this and recognize it as a real production interface, not a generated mockup?

---

## Positive Directives

These replace the prohibited patterns with better defaults:

**Instead of gradient text** → Use weight, size, and letter-spacing contrast. A 700-weight display font at 64px with a 400-weight body at 16px is more distinctive than any gradient.

**Instead of status badges** → Use position, hierarchy, and whitespace to signal priority. A pinned item at the top of a list does not need a "PINNED" label.

**Instead of ambient animation** → Use stillness as a design feature. Interfaces that don't move feel confident. Add motion only at moments of state change.

**Instead of boilerplate layouts** → Start with the content. Write the real copy first (or approximate it honestly), then design the container around what the words and data actually need.

**Instead of decorative shapes** → Use negative space. The absence of an element is also a design decision.

---

## Working with `frontend-design`

This skill and `frontend-design` operate on different axes:

- **`frontend-design`** → *What* to design (palette, type, signature element, aesthetic direction)
- **`anti-slop-ui`** → *What not to produce* (prohibited patterns, quality gate, anti-defaults)

Read `frontend-design` for direction. Apply `anti-slop-ui` as a filter before and after writing code. If you only have one skill loaded and the user is asking for original UI work, bias toward `frontend-design`. If the user is asking you to clean up, review, or "make it look professional," this skill takes priority.
