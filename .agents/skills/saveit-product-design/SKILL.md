---
name: saveit-product-design
description: Apply SaveIt's established product flows, visual system, mascot rules, and accessibility constraints when designing, implementing, reviewing, or testing SaveIt Flutter UI. Use for any SaveIt screen, widget, navigation, Action, Check-in, Reminder, History, settings, or visual QA work.
---

# SaveIt Product Design

Preserve SaveIt as a compact, local-only, one-tap Action logger. Use the domain vocabulary in [`../../../CONTEXT.md`](../../../CONTEXT.md) and respect the accepted decisions under [`../../../docs/adr/`](../../../docs/adr/).

## Before changing UI

1. Read [`../../../docs/design/design-system.md`](../../../docs/design/design-system.md) for visual tokens, components, mascot behavior, responsive rules, motion, and accessibility.
2. Read [`../../../docs/design/product-flows.md`](../../../docs/design/product-flows.md) when work changes navigation, state, persistence, permissions, notifications, or cross-screen behavior.
3. Read [`../../../docs/design/screen-specs.md`](../../../docs/design/screen-specs.md) for every screen touched.
4. Inspect the selected visual reference at `../../../docs/design/assets/saveit-home-reference.png` and the mascot atlas plus JSON in `../../../assets/` when the work affects Home, snackbar, or mascot rendering.

## Invariants

- A tap on an Action creates a Check-in immediately; planning and editing stay off the hot path.
- Home positions remain stable until the person explicitly reorders them.
- SaveIt never creates a Reminder or Check-in merely because it inferred intent.
- Mascot poses add controlled warmth in the Home header and Check-in snackbar; functional meaning remains in text, icons, haptics, and semantics.
- Active navigation and the plus Action use flat solid fill. Preserve the selected reference's three-column signal-tile character without gradients or glow.
- Keep data local, request notification permission only during first Reminder save, and keep medicine copy non-clinical.

## Completion

Before handing off a UI change, verify the affected full flow at the highest available Flutter seam, keyboard/screen-reader semantics, 200% text scale, reduced motion, narrow phone, reference phone, and tablet. Compare rendered Home work directly with the selected visual reference and account for every intentional difference.
