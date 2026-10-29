# UI vocabulary: components

Canonical names for the components and patterns a screen is built from, so a request for a UI change names one concept precisely. The other UI files: [ui-layout.md](ui-layout.md), [ui-interaction.md](ui-interaction.md). Motion terms live in `emilkowalski-animation-vocabulary`; [ui-interaction.md](ui-interaction.md) adds only the motion terms missing there. Where a term shares a name with one of its motion terms (Skeleton, Accordion), the entry here names the element or state and the motion stays there.

## Language

### Components and patterns

#### Overlays

**Overlay**:
Umbrella term for any element that floats above the page: dialog, popover, tooltip, sheet, toast.[^nng-popups]
_Avoid_: Popup, modal (as umbrella)

**Dialog**:
An overlay window with its own task; it is modal by default.[^apg-dialog][^nng-modal]
_Avoid_: Modal (as a noun), popup, lightbox

**Modal**:
Property of an overlay: the page behind it is inert (no focus, no clicks, no scroll) until it closes.[^nng-modal][^mdn-inert]
_Avoid_: Blocking

**Non-modal dialog**:
A dialog that leaves the page behind it usable.[^nng-modal]
_Avoid_: Floating window, panel

**Alert dialog**:
A modal dialog that interrupts to ask for a confirmation or decision, usually for a destructive action.[^apg-alertdialog][^hig-alerts]
_Avoid_: Alert (bare), confirm popup, Apple "alert"

**Popover**:
A non-modal overlay anchored to its trigger that can hold interactive content and closes on outside click or Escape (light dismiss).[^mdn-popover][^hig-popovers]
_Avoid_: Dropdown, popup, tooltip

**Tooltip**:
A short text label that appears on hover or keyboard focus of an element, after a delay; it never holds interactive content.[^apg-tooltip][^nng-tooltip]
_Avoid_: Hint, popover, title attribute

**Toggletip**:
A small popover opened by clicking an info icon that shows a short explanation, for touch screens where hover does not exist.[^nng-tooltip]
_Avoid_: Popup tip, info tooltip

**Hover card**:
A rich preview of a link's destination (profile, page) that opens on hover after a delay; it is a visual extra, not reachable by touch.[^radix-hover-card][^base-ui-preview-card]
_Avoid_: Preview card (Base UI name), link preview

**Sheet**:
A dialog panel that slides in from one edge of the screen and covers part of the page.[^shadcn-sheet][^hig-sheets]
_Avoid_: Side panel, slide-over, off-canvas

**Drawer**:
A sheet that the user can drag: it follows the finger, rests at snap points and is dismissed by swiping.[^base-ui-drawer][^shadcn-drawer]
_Avoid_: Bottom sheet (when gestures matter), swipeable sheet

**Bottom sheet**:
A sheet or drawer anchored to the bottom edge, the common mobile form; often starts partly open and expands.[^nng-bottom-sheet][^hig-sheets]
_Avoid_: Action panel, mobile modal

**Snap point**:
A height at which a draggable sheet comes to rest, such as half-open or full.[^base-ui-drawer][^hig-sheets]
_Avoid_: Detent (Apple name), stop

**Grabber**:
The short horizontal bar at the top of a draggable sheet that shows it can be dragged.[^hig-sheets][^nng-bottom-sheet]
_Avoid_: Handle, drag indicator, pill

**Lightbox**:
A full-screen viewer for an enlarged image or media item over a dimmed page.[^nng-popups]
_Avoid_: Image modal, gallery popup

#### Menus and choosing

**Menu**:
A list of actions opened from a trigger; picking an item runs it and closes the menu.[^apg-menu-button][^hig-pull-down]
_Avoid_: Dropdown, dropdown menu, pull-down button

**Menu button**:
A button that opens a menu.[^apg-menu-button]
_Avoid_: Dropdown trigger, kebab (name the icon separately)

**Context menu**:
A menu opened by right-click or long-press at the pointer position.[^radix-context-menu]
_Avoid_: Right-click menu

**Split button**:
A button with a default action on its label and a separate arrow segment that opens a menu of alternatives.[^nng-split-button]
_Avoid_: Menu button (no default action), dropdown button

**Select**:
A control that shows the current value and opens a list from which exactly one option is picked; no typing.[^apg-combobox][^hig-pop-up][^base-ui-list]
_Avoid_: Dropdown, pop-up button, picker

**Combobox**:
A text input with an attached list that filters as the user types; the value must be one of the options.[^apg-combobox][^base-ui-autocomplete]
_Avoid_: Searchable select, typeahead, dropdown with search

**Autocomplete**:
A text input whose suggestions are optional: any typed text is a valid value.[^base-ui-autocomplete][^hig-combo-box]
_Avoid_: Combobox (when free text is allowed), suggest box

**Listbox**:
An always-visible list of options where one or more are selected.[^apg-listbox][^nng-listbox]
_Avoid_: Select list, multi-select box

**Command palette**:
A keyboard-opened searchable list of all actions and destinations (shadcn `Command`).[^shadcn-command]
_Avoid_: Command menu, quick switcher, spotlight

#### Messages

**Toast**:
A short, non-modal message that appears briefly in a corner and disappears on its own; it never carries the only copy of an error.[^nng-indicators][^base-ui-toast]
_Avoid_: Snackbar, notification popup, flash message

**Banner**:
A message strip across the full width of the page or app that stays until dismissed or resolved.[^convention]
_Avoid_: Alert bar, notice bar, toast; banner for the page header, which is the ARIA `banner` landmark (`<header>`)

**Callout**:
A static, styled box inside the content that draws attention to a note, warning or error (shadcn `Alert`).[^shadcn-alert]
_Avoid_: Alert (bare), notice, admonition

**Live announcement**:
A message that a screen reader reads out without moving focus (ARIA `alert` or `status` live region).[^apg-alert][^mdn-aria-live]
_Avoid_: Alert (bare), notification

**Badge**:
A small, non-interactive label showing a status or count; a count badge is the dot or number pinned to an icon's corner.[^shadcn-badge][^android-badge]
_Avoid_: Pill, tag, label

**Chip**:
A small interactive element for filtering, input tokens or suggestions; it can be selected or removed.[^android-chip]
_Avoid_: Pill, tag, badge (non-interactive)

#### Disclosure and grouping

**Disclosure**:
A button that shows and hides one section of content below it; React libraries call it Collapsible.[^apg-disclosure][^hig-disclosure]
_Avoid_: Collapsible, expander, toggle section

**Accordion**:
A stack of disclosure headers where each reveals its own panel, often with only one open at a time. Its height animation is `emilkowalski-animation-vocabulary`'s Accordion / Collapse.[^apg-accordion]
_Avoid_: Collapse list, FAQ toggles

**Tabs**:
A row of tab labels that switches between panels in the same place, one visible at a time.[^apg-tabs]
_Avoid_: Segmented control (switches a value, not panels), pills

**Segmented control**:
A row of equal, joined buttons that sets one value (or a few); built with a toggle group.[^hig-segmented][^radix-toggle-group]
_Avoid_: Toggle group (implementation), segmented button, button group

**Card**:
A bordered or raised container that groups the content and actions about one item.[^nng-cards]
_Avoid_: Tile, panel, box

**Toolbar**:
A row of related controls, grouped as one Tab stop and navigated with arrow keys.[^apg-toolbar]
_Avoid_: Action bar, button row

**Carousel**:
A set of slides shown one (or a few) at a time with previous/next controls.[^apg-carousel]
_Avoid_: Slider (a value control), slideshow, gallery

#### Controls

**Button emphasis**:
The visual weight of a button: primary (filled), secondary (outlined or tonal), ghost (no container), link-style.[^hig-buttons]
_Avoid_: Button type, button color

**Icon button**:
A button showing only an icon; it must have an accessible name.[^apg-button-name]
_Avoid_: Icon link, glyph button

**Switch**:
An on/off control that takes effect immediately.[^apg-switch][^hig-toggles]
_Avoid_: Toggle (bare), checkbox

**Checkbox**:
A control that marks an option on or off for submission later; it can show a mixed state.[^nng-checkbox-radio]
_Avoid_: Tick box, switch

**Toggle button**:
A button that stays On or Off until it is pressed again, such as Bold in an editor (`aria-pressed`).[^base-ui-list]
_Avoid_: Switch, active button, pressed (for its lasting On state)

**Slider**:
A control for picking a value along a track by dragging a thumb.[^base-ui-list]
_Avoid_: Range, carousel

**Number field**:
A text input for a number with − and + buttons that step it.[^nng-stepper][^base-ui-list]
_Avoid_: Stepper (also means wizard steps), spinbutton, counter

**Progress bar**:
A bar that shows how far a task has advanced; it is indeterminate when the total is unknown.[^hig-progress][^nng-progress]
_Avoid_: Loader, meter

**Meter**:
A bar that shows a measured value within a known range, such as disk usage or a quota.[^apg-meter]
_Avoid_: Progress bar, gauge

**Spinner**:
An indeterminate rotating indicator for a short wait whose length is unknown.[^nng-progress][^nng-skeleton]
_Avoid_: Loader, throbber, activity indicator

**Avatar**:
A small image or initials that represent a person or account.[^base-ui-list]
_Avoid_: Profile picture, userpic

**Scroll area**:
A region with its own custom-styled scrollbar.[^base-ui-list]
_Avoid_: Scroll box, overflow container

[^apg-dialog]: APG Dialog (Modal): https://www.w3.org/WAI/ARIA/apg/patterns/dialog-modal/ (URL 200)
[^apg-alertdialog]: APG Alert Dialog: https://www.w3.org/WAI/ARIA/apg/patterns/alertdialog/ (URL 200)
[^apg-tooltip]: APG Tooltip, a work-in-progress pattern: https://www.w3.org/WAI/ARIA/apg/patterns/tooltip/ (read)
[^apg-combobox]: APG Combobox, including select-only combobox and autocomplete modes: https://www.w3.org/WAI/ARIA/apg/patterns/combobox/ (read)
[^apg-listbox]: APG Listbox: https://www.w3.org/WAI/ARIA/apg/patterns/listbox/ (URL 200)
[^apg-menu-button]: APG Menu Button: https://www.w3.org/WAI/ARIA/apg/patterns/menu-button/ (URL 200)
[^apg-disclosure]: APG Disclosure: https://www.w3.org/WAI/ARIA/apg/patterns/disclosure/ (read)
[^apg-accordion]: APG Accordion: https://www.w3.org/WAI/ARIA/apg/patterns/accordion/ (URL 200)
[^apg-tabs]: APG Tabs: https://www.w3.org/WAI/ARIA/apg/patterns/tabs/ (URL 200)
[^apg-switch]: APG Switch: https://www.w3.org/WAI/ARIA/apg/patterns/switch/ (URL 200)
[^apg-alert]: APG Alert: https://www.w3.org/WAI/ARIA/apg/patterns/alert/ (read)
[^apg-meter]: APG Meter: https://www.w3.org/WAI/ARIA/apg/patterns/meter/ (URL 200)
[^apg-toolbar]: APG Toolbar: https://www.w3.org/WAI/ARIA/apg/patterns/toolbar/ (URL 200)
[^apg-carousel]: APG Carousel: https://www.w3.org/WAI/ARIA/apg/patterns/carousel/ (URL 200)
[^apg-button-name]: APG Button pattern (accessible name), listed on the patterns index: https://www.w3.org/WAI/ARIA/apg/patterns/ (read)
[^mdn-popover]: MDN Popover API; the page names the `auto`/`manual`/`hint` states but does not define them in detail: https://developer.mozilla.org/en-US/docs/Web/API/Popover_API (read)
[^mdn-aria-live]: MDN `aria-live`: https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/Reference/Attributes/aria-live (URL 200)
[^mdn-inert]: MDN `inert`: https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Global_attributes/inert (URL 200)
[^radix-hover-card]: Radix Hover Card, "intended for sighted users only": https://www.radix-ui.com/primitives/docs/components/hover-card (read)
[^radix-context-menu]: Radix Context Menu: https://www.radix-ui.com/primitives/docs/components/context-menu (URL 200)
[^radix-toggle-group]: Radix Toggle Group: https://www.radix-ui.com/primitives/docs/components/toggle-group (URL 200)
[^base-ui-list]: Base UI component list (Field, Fieldset, Number Field, OTP Field, Toggle, Separator, Scroll Area, Avatar, Select, Slider): https://base-ui.com/react/overview/quick-start (read)
[^base-ui-preview-card]: Base UI Preview Card, opens on hover or focus after a delay: https://base-ui.com/react/components/preview-card (read)
[^base-ui-autocomplete]: Base UI Autocomplete compared with Combobox: https://base-ui.com/react/components/autocomplete (read; first 100k characters)
[^base-ui-drawer]: Base UI Drawer (swipe, snap points, indent, modal by default): https://base-ui.com/react/components/drawer (read)
[^base-ui-toast]: Base UI Toast: https://base-ui.com/react/components/toast (URL 200)
[^shadcn-sheet]: shadcn Sheet, built on Dialog and opening from any edge: https://ui.shadcn.com/docs/components/sheet (read)
[^shadcn-drawer]: shadcn Drawer, now built on Base UI with swipe and snap points: https://ui.shadcn.com/docs/components/drawer (read)
[^shadcn-alert]: shadcn Alert, a callout: https://ui.shadcn.com/docs/components/alert (read)
[^shadcn-badge]: shadcn Badge: https://ui.shadcn.com/docs/components/base/badge (URL 200)
[^shadcn-command]: shadcn Command: https://ui.shadcn.com/docs/components/base/command (URL 200)
[^hig-sheets]: Apple HIG Sheets (modal and nonmodal, detents, grabber): https://developer.apple.com/design/human-interface-guidelines/sheets (read via the JSON data endpoint)
[^hig-popovers]: Apple HIG Popovers: https://developer.apple.com/design/human-interface-guidelines/popovers (read)
[^hig-alerts]: Apple HIG Alerts: https://developer.apple.com/design/human-interface-guidelines/alerts (read)
[^hig-segmented]: Apple HIG Segmented controls: https://developer.apple.com/design/human-interface-guidelines/segmented-controls (read)
[^hig-toggles]: Apple HIG Toggles: https://developer.apple.com/design/human-interface-guidelines/toggles (read)
[^hig-pull-down]: Apple HIG Pull-down buttons: https://developer.apple.com/design/human-interface-guidelines/pull-down-buttons (read)
[^hig-pop-up]: Apple HIG Pop-up buttons: https://developer.apple.com/design/human-interface-guidelines/pop-up-buttons (read)
[^hig-combo-box]: Apple HIG Combo boxes, which accept custom text: https://developer.apple.com/design/human-interface-guidelines/combo-boxes (read)
[^hig-progress]: Apple HIG Progress indicators, determinate and indeterminate: https://developer.apple.com/design/human-interface-guidelines/progress-indicators (read)
[^hig-disclosure]: Apple HIG Disclosure controls: https://developer.apple.com/design/human-interface-guidelines/disclosure-controls (read)
[^android-chip]: Android Compose Chip (assist, filter, input, suggestion): https://developer.android.com/develop/ui/compose/components/chip (read)
[^android-badge]: Android Compose Badges: https://developer.android.com/develop/ui/compose/components/badges (URL 200)
[^nng-modal]: NN/g Modal and nonmodal dialogs: https://www.nngroup.com/articles/modal-nonmodal-dialog/ (read)
[^nng-popups]: NN/g Popups (overlay, lightbox, modal and nonmodal): https://www.nngroup.com/articles/popups/ (read)
[^nng-tooltip]: NN/g Tooltip guidelines (tooltip compared with popup tip): https://www.nngroup.com/articles/tooltip-guidelines/ (read)
[^nng-indicators]: NN/g Indicators, validations and notifications (toast): https://www.nngroup.com/articles/indicators-validations-notifications/ (read)
[^nng-skeleton]: NN/g Skeleton screens compared with spinners and progress bars: https://www.nngroup.com/articles/skeleton-screens/ (read)
[^nng-bottom-sheet]: NN/g Bottom sheets (modal, nonmodal, grabber, scrim): https://www.nngroup.com/articles/bottom-sheet/ (read)
[^nng-listbox]: NN/g Listbox compared with dropdown list: https://www.nngroup.com/articles/listbox-dropdown/ (read)
[^nng-split-button]: NN/g Split buttons: https://www.nngroup.com/articles/split-buttons/ (read)
[^nng-stepper]: NN/g Input steppers: https://www.nngroup.com/articles/input-steppers/ (read)
[^nng-progress]: NN/g Progress indicators: https://www.nngroup.com/articles/progress-indicators/ (URL 200)
[^nng-checkbox-radio]: NN/g Checkboxes compared with radio buttons: https://www.nngroup.com/articles/checkboxes-vs-radio-buttons/ (URL 200)
[^nng-cards]: NN/g Cards: https://www.nngroup.com/articles/cards-component/ (URL 200)
[^hig-buttons]: Apple HIG Buttons (prominent and less prominent styles): https://developer.apple.com/design/human-interface-guidelines/buttons (read)
[^convention]: None of the primary sources consulted names this concept; the name comes from common practice, and the owner chose it on 2026-10-28.
