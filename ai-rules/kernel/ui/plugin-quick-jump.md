# Plugin Quick Jump Rule

Tool: codex

## Purpose

This rule standardizes Vim-style target-hint quick jump for plugin products. It comes from EyPc's `f` quick-jump iteration and is reusable only for dense plugin/workbench surfaces where keyboard-first navigation is part of the product model.

## Scope

Use this rule for plugin-like products:

- uTools plugins, browser-extension popups or side panels, IDE/editor panels, desktop plugin panels, embedded workbenches, and other host-shell command surfaces.
- Dense operational panes where visible controls, lists, records, and per-item actions must be reachable without pointer movement.

Do not apply it by default to ordinary websites, landing pages, marketing pages, content pages, games, or general web apps. For those surfaces, use normal accessibility, tab order, command palette, or local shortcuts unless the user explicitly asks for Vim-style hints.

## Command Contract

- `F` opens forward Quick Jump only when the current owner is a non-editing app surface.
- `Shift+F` may open reverse or alternate-direction Quick Jump when the product has a meaningful reverse target set.
- Inputs, textareas, contenteditable editors, code editors, and elements with textbox/searchbox/editor roles must keep their native `f` typing behavior.
- `Escape` closes the hint layer before broader app-level Escape handling.
- `Enter` activates the active target when a query has narrowed to one target.
- Arrow keys and product-standard navigation keys may move the active target without leaving Quick Jump.
- `Backspace` edits the query. Empty query returns to the full visible target set.
- The marker alphabet must exclude the trigger key itself and must avoid host-reserved or project-reserved command letters when they would cause ambiguity.
- Markers must be deterministic and prefix-safe. Prefer fixed-width markers or an explicit prefix-free generator so typing a marker cannot partially activate a different target.
- Marker matching uses the full marker, but the visible overlay should hide already typed marker-prefix letters. For example, after typing `a`, targets `aa`, `as`, and `ad` should display `a`, `s`, and `d` as the remaining keys.

## Target Model

Quick Jump targets are current visible actions and selectable objects, not every element in the DOM.

Include:

- Visible enabled buttons and icon buttons.
- Focusable text controls such as inputs, textareas, search boxes, and ARIA textbox/searchbox elements when Quick Jump opens from a non-editing surface. Once focused, those controls must block global `F` and keep native typing.
- Links and menu items only when the plugin uses them as primary commands.
- Explicit command targets such as `[data-quick-jump-target]`, project shortcut metadata, `role="button"`, `role="menuitem"`, `role="option"`, and `role="treeitem"`.
- Selectable rows, records, cards, or connection items when clicking the item selects, focuses, opens, or highlights it.

Skip:

- Hidden, disabled, `aria-hidden`, `aria-disabled`, offscreen, clipped, transparent, collapsed, or pointer-blocked controls.
- Buttons hidden in overflow menus or panels that are not currently displayed.
- Targets whose visible rectangle is too small or whose center is outside the viewport after clipping checks.
- Decorative icons, repeated static labels, non-action text, and passive layout containers.
- Targets inside an editing surface unless the surface explicitly exposes command buttons as Quick Jump targets.

When a button is not displayed, do not show its jump letters. Hidden action capacity should not leak through the hint layer.

## Item Markers

Whole records and rows should be jumpable when the product already treats the item itself as selectable.

- Item marker placement should anchor near the item title or primary label, slightly to the right of the title.
- Prefer an explicit title anchor such as `[data-quick-jump-anchor]` when item layout has many badges, action buttons, or virtualized columns.
- The marker should activate the item selection/focus/open behavior, not a random child action.
- Per-item action buttons may still have their own markers, but they must not obscure the item marker.

This keeps item selection close to the user's visual model: title first, actions second.

## Visual Taste

The hint layer is a transient command overlay, not part of the component layout.

- Render markers in a fixed top-layer portal with a z-index above plugin content and scroll containers.
- Markers must not reflow, resize, or restyle the source control.
- Default placement for normal buttons is slightly above the target center, with viewport clamping.
- Row and record markers use the item-title placement rule above.
- Large buttons, text controls, and row surfaces should use their internal whitespace before falling back to a shared center point, and marker layout should avoid overlapping nearby markers when enough space exists.
- Clamp markers inside the viewport and avoid clipping by rounded panels, scroll panes, and overflow-hidden containers.
- Prefer transparent, lightweight red-purple text with enough contrast over the real UI. Avoid filled badge backgrounds unless contrast or brand tokens require them.
- Keep the overlay visually distinct from product chrome while remaining quiet enough not to hide the workflow.
- If text is covered or cropped, change placement before increasing opacity or adding containers.

## Runtime Ownership

Quick Jump is owned by explicit app command state.

- Do not infer command eligibility from DOM focus alone in host-shell or embedded-browser products.
- Track whether the current layer is editing, modal, menu, drag, composition, or normal app surface.
- During IME composition, text selection, drag, resize, or modal confirmation, do not open global Quick Jump unless that layer explicitly owns the command.
- Activation should reuse the original target's command path: focus/click/dispatch the same handler boundary rather than duplicating business logic.

## Implementation Notes

- Keep the marker generator pure and unit-testable.
- Keep full marker matching separate from display labels so prefix consumption does not mutate target identity or activation behavior.
- Keep marker layout testable enough to prove viewport clamping and non-overlap behavior for large targets.
- Keep target scanning isolated from rendering.
- Prefer `getBoundingClientRect()` plus computed style and clipping checks over CSS-selector-only visibility tests.
- Virtualized lists should scan only mounted visible rows and refresh targets after scroll, filter, or resize.
- Debounce only expensive rescans; activation should remain immediate.
- When target count is large, keep query filtering fast and predictable before adding fuzzy matching.

## Verification

For plugin projects implementing or changing Quick Jump, verify at least:

- `F` opens only from non-editing surfaces; typing `f` in inputs, textareas, search boxes, and editors still enters text.
- `Escape`, `Enter`, `Backspace`, and navigation keys behave according to the command contract.
- Hidden, clipped, disabled, offscreen, and undisplayed overflow buttons do not receive markers.
- Visible rows/records can be selected through item markers placed near their titles.
- Focusable text controls are covered from non-editing context but still block `F` once focused.
- Marker labels are not cropped, hidden behind panels, or clipped by scroll containers.
- Large targets with enough internal space do not stack multiple markers on the same center point.
- The trigger key is excluded from generated markers, and marker activation is deterministic.
- Multi-letter marker prefixes consume their visible prefix and display only the unresolved suffix while preserving full-marker exact activation.
- A screenshot, DOM overlay check, or Playwright/browser test covers at least one real plugin surface when feasible.

Route project-specific command IDs, selectors, marker alphabet choices, colors, and screenshots to the project rule or task docs. Keep this master file limited to reusable plugin behavior.
