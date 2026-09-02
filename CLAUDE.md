# Drift Field — Design Rules

## Corner stack system

All persistent UI elements live inside one of four CSS flex corner containers:

| Container    | CSS class          | Flex direction    | Anchor position |
|--------------|--------------------|-------------------|-----------------|
| `#corner-tl` | `.corner-tl`       | `column`          | First DOM child |
| `#corner-tr` | `.corner-tr`       | `column`          | First DOM child |
| `#corner-bl` | `.corner-bl`       | `column-reverse`  | First DOM child |
| `#corner-br` | `.corner-br`       | `column-reverse`  | First DOM child |

**Every corner element — cards, the reset button, and the wordmark — belongs inside a corner container. No UI element uses its own `position: fixed` independently.**

- `gap: 20px` between elements in every corner stack (matches the 20px viewport margin).
- All corners sit exactly 20px from the viewport edge (`top/bottom/left/right: 20px`).

### Current permanent anchors
- `#corner-tl` — hint card (draggable)
- `#corner-tr` — "Clear field" reset button (non-draggable)
- `#corner-bl` — wordmark / logo (non-draggable)
- `#corner-br` — legend card (draggable)

## Drag and snap rules

### Anchor vs. second place
- First DOM child of a container = **anchor** (closest to corner edge — CSS flex places it there naturally).
- Use `container.prepend(el)` to make a card the anchor.
- Use `container.appendChild(el)` to stack a card in second place.

### Snap zones (on pointer release)
| Distance from corner | Behaviour |
|---|---|
| < 130 px | Card becomes **anchor** (`prepend`) |
| 130 – 260 px | Card slots **second place** (`appendChild`) |
| > 260 px | Card stays **floating**, no snap |

### Auto-slot
When the anchor card is dragged away from a corner, the next card in the flex container automatically slides into the anchor slot — no JS required, CSS flex reflow handles it.

### Flip
Dragging a card into a corner that already has an anchor always **prepends** — the incoming card becomes the new anchor and the existing anchor shifts to second.

## Zero overlap
CSS flex containers guarantee no overlap. Never use JS-calculated positions for card layout within a corner.

## Text color
All card text: `#26251f`.
