# The Comfort Table

> An interactive comfort-food editorial experience built with semantic HTML, expressive CSS, vanilla JavaScript, and accessibility-first interaction design.

[![Live Demo](https://img.shields.io/badge/Live-Demo-315846?style=for-the-badge)](https://the-comfort-table.vercel.app/)
[![Challenge](https://img.shields.io/badge/DEV-Frontend%20Challenge-d76a2d?style=for-the-badge)](https://dev.to/bugsmash)

## Overview

**The Comfort Table** turns comfort food into a small interactive story rather than another static menu. Visitors choose a mood and moment, discover a matching dish, explore a global menu, and open detailed dish stories.

The project was originally built for DEV's Frontend Challenge: Comfort Food Edition and has since been hardened through a focused accessibility bug fix for the DEV Bug Smash campaign.

## The Bug Smash Fix

The project used a custom modal with `role="dialog"` and `aria-modal="true"`, but the accessibility semantics were stronger than the underlying interaction lifecycle.

The hardening work addressed the modal as an actual modal interaction rather than treating ARIA attributes as a substitute for behavior.

### Fixed behavior

- initial focus is moved into the dialog
- `Tab` and `Shift+Tab` are contained within the dialog
- `Escape` closes the dialog
- focus is restored to the element that opened the dialog
- background content is made inert while the dialog is open
- overlay interaction is handled consistently
- modal open/close state is managed as one lifecycle

### Why it matters

A component should not claim to be modal while still allowing keyboard or assistive-technology users to interact with the page behind it. The fix aligns the implementation with the expected behavior of a modal dialog while preserving the existing visual design and responsive layout.

## Verification Status

| Area | Status | Evidence |
| --- | --- | --- |
| Repository fix | ✅ | `62a7f04` — `fix: harden modal accessibility` |
| Main application | ✅ | `index.html` contains the hardened modal lifecycle |
| Responsive UI | ✅ | Mobile layout tested manually |
| Modal open/close | ✅ | Manual mobile verification |
| Overlay behavior | ✅ | Manual mobile verification |
| Refresh/repeated interaction | ✅ | Manual mobile verification |
| Keyboard `Tab` / `Shift+Tab` | ⚠️ | Desktop verification still recommended |
| Escape keyboard behavior | ⚠️ | Desktop keyboard verification still recommended |
| Focus restoration | ⚠️ | Desktop keyboard verification still recommended |

> **Evidence policy:** this table deliberately distinguishes implemented behavior from independently verified behavior. Unverified desktop keyboard checks are not represented as completed tests.

## Accessibility Baseline

The application already includes several accessibility foundations:

- semantic HTML structure
- skip-to-content link
- accessible navigation labels
- `aria-pressed` state for interactive selectors
- `aria-live` recommendation updates
- visible `:focus-visible` styling
- `prefers-reduced-motion` support
- touch-friendly controls
- responsive layouts

The Bug Smash work focuses specifically on the custom dialog lifecycle, where behavioral accessibility is more important than simply adding ARIA attributes.

## Design & UX

The experience uses a restrained food-memory visual system: paper, cream, terracotta, saffron, and deep green. The hero illustration is generated with CSS rather than stock artwork.

The primary interaction is intentionally simple:

```text
Choose mood + moment
        ↓
Receive a comfort-food recommendation
        ↓
Explore the world menu
        ↓
Open a dish story
        ↓
Return to the exact place that launched the dialog
```

## Features

- Responsive mobile/tablet/desktop layout
- CSS-generated hero food illustration
- Interactive comfort finder
- Global dish menu
- Country and text filtering
- Dish detail modal
- Semantic HTML
- Keyboard-visible focus states
- `aria-pressed` controls
- `aria-live` dynamic recommendation updates
- Reduced-motion support
- No external runtime dependency
- Touch-friendly controls
- Multilingual interface
- CSS-generated artwork

## Project Structure

```text
.
├── index.html
├── css-art.html
├── README.md
├── DEV-SUBMISSION.md
└── QA_RELEASE_GATE.md
```

## Local Development

This is a static frontend and requires no build system.

```bash
git clone https://github.com/pawansatoshi/the-comfort-table.git
cd the-comfort-table
python3 -m http.server 8080
```

Then open `http://localhost:8080` in a browser.

## Live Demo

**[Open The Comfort Table](https://the-comfort-table.vercel.app/)**

## Bug Smash Submission

This repository contains the implementation and supporting evidence for the **DEV Bug Smash — Clear the Lineup** submission.

See [`DEV-SUBMISSION.md`](DEV-SUBMISSION.md) for the judge-facing technical summary and [`QA_RELEASE_GATE.md`](QA_RELEASE_GATE.md) for the release checklist.

## Engineering Principle

The project follows a simple rule for accessibility work:

> **ARIA should describe real behavior, not replace it.**

When a component declares itself as a modal, its focus, keyboard, background-interaction, and close lifecycle should behave like a modal.

## License

No open-source license is currently declared for this repository. Until a license is added, existing copyright and repository terms apply.

---

Built for the DEV Frontend Challenge and hardened for DEV Bug Smash by **Pawan Satoshi**.