# DEV Bug Smash — Clear the Lineup

## Project

**The Comfort Table**

Live demo: https://the-comfort-table.vercel.app/

Repository: https://github.com/pawansatoshi/the-comfort-table

## The Bug

The application used a custom dialog with `role="dialog"` and `aria-modal="true"`, but the interaction behavior did not fully implement the modal contract.

The main gap was that the dialog semantics existed without a complete focus-management lifecycle. For keyboard and assistive-technology users, that can allow focus to escape the intended dialog boundary and can leave focus in an unexpected place after closing.

## Why This Was a Real Bug

A modal is not made accessible simply by adding ARIA attributes.

When a component declares itself as `aria-modal="true"`, users should be able to:

1. enter the dialog with focus inside it
2. move through interactive controls without escaping into the page behind it
3. close the dialog with `Escape`
4. return focus to the control that opened it
5. have the background treated as unavailable while the modal is active

The original implementation did not provide that complete lifecycle.

## Root Cause

The UI used a custom `div` dialog rather than a native dialog element. The existing implementation managed visual open/close state, but focus containment, focus restoration, and background inertness were not treated as one lifecycle.

That created a mismatch between the declared accessibility semantics and the actual interaction model.

## The Fix

Commit: `62a7f04` — `fix: harden modal accessibility`

The modal lifecycle was hardened to provide:

- initial focus inside the dialog
- `Tab` focus containment
- `Shift+Tab` reverse containment
- `Escape` close behavior
- focus restoration to the invoking element
- background inertness while open
- consistent overlay close behavior
- explicit open/close lifecycle management

The fix was designed to preserve the existing visual and responsive experience rather than replacing the component with a different UI pattern.

## Before vs After

### Before

The application visually presented a modal and exposed `role="dialog"` / `aria-modal="true"`, but the behavioral lifecycle was incomplete.

### After

The modal is treated as an interaction boundary:

```text
invoking button
      ↓
open modal
      ↓
move focus inside
      ↓
contain Tab / Shift+Tab
      ↓
Escape or close
      ↓
restore focus to invoking button
```

Background content is also made inert while the dialog is active.

## Verification

### Manually verified on mobile

- modal opens from dish details
- modal closes with the close control
- overlay interaction behaves correctly
- repeated open/close cycles work
- browser refresh does not leave the interface in a broken modal state
- responsive layout remains usable

### Desktop keyboard verification

The implementation includes the keyboard lifecycle described above. A desktop keyboard pass for `Tab`, `Shift+Tab`, `Escape`, and focus restoration is recommended as an additional independent verification step.

This submission intentionally does **not** claim that those desktop checks were manually performed when they were not.

## Accessibility Foundations Already Present

The application also includes:

- semantic HTML
- skip-to-content navigation
- accessible navigation labels
- visible keyboard focus styles
- `aria-pressed` state for mood/time controls
- `aria-live` dynamic recommendation output
- `prefers-reduced-motion` support
- touch-friendly controls
- responsive mobile/tablet/desktop layout

## Impact

The fix improves the experience for keyboard users and users of assistive technologies while also making the component's implementation more internally consistent.

The broader engineering lesson is simple:

> **ARIA should describe real behavior, not replace it.**

## Scope

This submission is a bug-fix/optimization of an existing application. The work does not depend on adding a new product feature; it hardens an existing interactive component and brings its behavior closer to its declared accessibility semantics.

## Files

Primary implementation:

- `index.html`

Supporting documentation:

- `README.md`
- `QA_RELEASE_GATE.md`
- `DEV-SUBMISSION.md`

## Links

- Live demo: https://the-comfort-table.vercel.app/
- GitHub: https://github.com/pawansatoshi/the-comfort-table
- Accessibility fix commit: https://github.com/pawansatoshi/the-comfort-table/commit/62a7f04a88d798c0dc6221f7c647b344f84f221b

## Submission Tag

`#bugsmash`

## Final Note

The project is intentionally transparent about verification status. Mobile behavior has been manually verified; desktop keyboard verification remains an explicit recommended final QA pass rather than an unsupported claim.