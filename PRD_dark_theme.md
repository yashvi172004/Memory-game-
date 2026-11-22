# PRD: Dark Theme for Memory Game

## Summary

Add a user-selectable dark theme to the existing memory game while preserving all current game behavior, layouts, scoring, and accessibility.

The feature will live in the existing `memory-game.html` implementation. It must not require a backend, build process, external package, or third-party library.

## Problem

The game currently uses a fixed light visual theme. Players who prefer low-light interfaces, use the game in dark environments, or have light sensitivity need a dark theme that remains readable and usable.

## Goals

- Provide clear light and dark visual themes.
- Let the player switch themes at any time without restarting or affecting the active game.
- Respect the player's preferred theme across browser sessions.
- Preserve the existing 4x4 and 6x6 game modes, timer, moves, rating, win dialog, keyboard controls, and best scores.
- Maintain or improve readability and accessibility in both themes.

## Non-Goals

- No redesign of the game layout or card artwork.
- No additional theme choices beyond light and dark.
- No backend, account system, or server-side preference storage.
- No change to matching rules, shuffle behavior, score sorting, or score limits.
- No changes to the current symbol sets.

## User Experience

### Theme Control

- Add a clearly labeled theme control near the grid size controls or in the page header.
- The control must be usable with a mouse and keyboard.
- Recommended initial UI: a button with text such as "Dark Theme" and an icon or state indicator.
- Clicking or activating the control toggles between light and dark mode.
- Update the control label and accessible name to describe the action or current state.
- Theme changes must take effect immediately and must not reset the timer, moves, selected cards, or active match delay.

### Initial Theme Selection

The initial theme should be selected in this order:

1. A previously saved theme preference, if present.
2. The operating system's `prefers-color-scheme` setting.
3. Light mode as the fallback.

Suggested browser-storage key: `memoryGameTheme`.

Suggested stored values:

- `light`
- `dark`

### Persistence

- Save the selected theme when the user toggles it.
- Restore the saved theme on page load.
- Use `localStorage` safely so unavailable or malformed storage does not prevent the game from loading.
- Do not alter or remove the existing `memoryGameScores` local-storage key.

## Visual Requirements

Implement theme colors using CSS custom properties or a small theme-state data attribute/class on the document root.

At minimum, theme-aware values must cover:

- Page background and text color.
- Primary button and active control colors.
- Controls panel background and border or shadow color.
- Card front and card back colors.
- Card text and card border or shadow colors.
- Win modal backdrop and modal content colors.
- Focus and hover states.
- Rating and status text.
- Best-scores panel.

The two themes must meet these principles:

- Maintain a strong text-to-background contrast ratio.
- Keep card backs visually distinct from card fronts.
- Keep the active grid-size control visually distinct.
- Preserve clear card, modal, and panel boundaries.
- Maintain visible keyboard focus indicators.
- Avoid using color alone to communicate active or matched states.
- Preserve existing card flip animations and 3D effects.

## Accessibility Requirements

- Theme control must be reachable in the normal keyboard tab order.
- Theme control must use an accessible label, for example "Switch to dark theme".
- Update the label or accessible state after theme changes.
- If a checkbox or switch pattern is used, expose its state with an appropriate ARIA attribute.
- Do not remove or obscure existing ARIA live regions.
- Modal behavior and focus treatment must remain unchanged.
- Theme changes must not trigger unexpected announcements or timer resets.
- Respect `prefers-reduced-motion` by reducing or disabling the card transition when appropriate.

## Technical Requirements

- Use existing HTML, CSS, and JavaScript conventions in `memory-game.html`.
- Keep the implementation dependency-free.
- Define theme variables for the light and dark palettes.
- Apply the selected theme before the first visible paint where practical to reduce theme flashing.
- Initialize theme state safely before game initialization.
- Add theme code alongside existing DOM element setup and event listeners.
- Guard storage read and write operations against exceptions.
- No game-state variables outside `gameState` should be changed unless necessary.

## Acceptance Criteria

1. A clearly visible theme control is present on the page.
2. The control switches the page from light to dark mode and from dark to light mode.
3. The selected theme is restored after refreshing or reopening the page.
4. With no saved preference, the system theme preference is followed where supported.
5. Toggling the theme does not reset moves, elapsed time, game mode, first-card state, matched cards, or pending mismatch behavior.
6. Switching grids while dark mode is active keeps the dark theme applied.
7. The win modal, play-again button, best-scores list, buttons, cards, and text remain readable in both themes.
8. The theme control works with mouse, Enter, and Space activation.
9. Existing keyboard card activation works after theme changes.
10. Existing best scores remain available and continue to work after theme changes.
11. The application loads normally when local-storage access is unavailable or contains an invalid theme value.
12. No external assets or network dependencies are introduced.
13. The page remains responsive at desktop and mobile widths.

## Regression Testing

Verify the existing feature set after implementation:

- Start a new 4x4 game.
- Complete 4x4 card selection and matching flows.
- Start a 6x6 game.
- Verify timer start, moves increment, rating update, mismatches, and matched-card handling.
- Complete both grid sizes to confirm win modal and score saving.
- Reload the page and verify theme and best scores persist.
- Verify theme switching mid-game and mid-mismatch.
- Verify keyboard navigation and activation.
- Verify light/dark appearance at desktop and narrow viewport widths.
- Verify behavior with `localStorage` unavailable or containing an unknown theme value.

## Implementation Completion Notes

After implementation, update directly relevant documentation only if needed. Include no broad refactor or unrelated behavior change.

Before completion, record:

- Which theme control was added.
- Where theme variables are defined.
- Which storage key is used.
- Whether system preference support was included.
- Which files changed.
