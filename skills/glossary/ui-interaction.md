# UI vocabulary: states, navigation, forms, motion and accessibility

Canonical names for how a screen responds, moves between places, takes input and stays accessible, so a request for a UI change names one concept precisely. The other UI files: [ui-layout.md](ui-layout.md), [ui-components.md](ui-components.md). Motion terms live in `emilkowalski-animation-vocabulary`; this file adds only the motion terms missing there. Where a term shares a name with one of its motion terms (Skeleton, Accordion), the entry here names the element or state and the motion stays there.

## Language

### States and feedback

**Rest state**:
How a control looks with no interaction.[^convention]
_Avoid_: Default state, normal, idle

**Hover state**:
How a control looks while a pointer is over it; it does not exist on touch screens.[^mdn-media-hover]
_Avoid_: Hover effect (that is the motion), mouse-over

**Focus**:
The element that receives keyboard input.[^apg-keyboard]
_Avoid_: Selection, active element (DOM name)

**Focus-visible**:
The visible focus ring shown when focus came from the keyboard and hidden after a mouse click, via `:focus-visible`.[^mdn-focus-visible]
_Avoid_: Focus outline, focus (when only the ring is meant)

**Pressed state**:
How a control looks while it is being pressed (CSS `:active`).[^m3-state-layer]
_Avoid_: Active state, click state

**Selected**:
The item chosen in a set (tab, option, chip), shown by a lasting highlight.[^apg-tabs][^apg-listbox]
_Avoid_: Active, current (for navigation), checked

**Current**:
The navigation item that matches the page the user is on (`aria-current`).[^apg-breadcrumb]
_Avoid_: Active link, selected (for navigation)

**Expanded**:
The open state of a disclosure, accordion section, menu or combobox (`aria-expanded`).[^apg-disclosure]
_Avoid_: Open (as attribute), active

**Disabled**:
A control that cannot be used and is skipped by Tab, and whose value is not submitted.[^mdn-disabled]
_Avoid_: Greyed out, inactive

**Focusable disabled**:
A control announced and styled as unavailable but still reachable by Tab, so its reason can be read (`aria-disabled`).[^mdn-aria-disabled]
_Avoid_: Soft disabled, fake disabled

**Read-only**:
A field whose value can be seen, focused, selected and submitted but not edited.[^mdn-readonly]
_Avoid_: Disabled, locked, non-editable

**Indeterminate**:
A checkbox in a mixed state (some children checked), or a progress indicator with no known total.[^hig-progress]
_Avoid_: Partial, half-checked

**Loading state**:
What a region shows while its data is on the way: skeleton, spinner, or progress bar.[^nng-skeleton]
_Avoid_: Loader, waiting screen

**Skeleton**:
A placeholder in the shape of the content that is about to load: grey blocks in its layout. The shimmer on it is `emilkowalski-animation-vocabulary`'s Skeleton / Shimmer.[^nng-skeleton][^shadcn-skeleton]
_Avoid_: Ghost UI, placeholder loader, shimmer (that is the motion)

**Pending state**:
A control's state after the user acts while the result is not yet confirmed: label kept, spinner inside, repeat clicks blocked.[^convention]
_Avoid_: Loading button, busy button

**Optimistic update**:
Showing the expected result of an action at once and rolling it back if the server rejects it.[^react-use-optimistic]
_Avoid_: Fake success, instant UI

**Empty state**:
What a region shows when it has nothing to show yet, with a reason and a next action; the no-results variant is a filter or search that matched nothing.[^nng-empty][^shadcn-empty]
_Avoid_: Zero state, blank state, null state

**Error state**:
How a region or field looks when an operation failed or input is invalid, with the cause and a recovery step.[^nng-form-errors]
_Avoid_: Failure screen, red state

**Hover intent delay**:
The pause before a hover-opened overlay (tooltip, hover card, submenu) opens or closes, so passing the pointer over it does nothing.[^base-ui-preview-card][^wcag-hover-focus]
_Avoid_: Hover timeout, debounce

### Navigation and scroll

**Top bar**:
The bar across the top of a page or app that holds the title, main navigation and global actions.[^convention]
_Avoid_: Header (also the page's `<header>`), navbar, app bar

**Tab bar**:
The bar of top-level destinations fixed to the bottom of a mobile screen.[^hig-tab-bars]
_Avoid_: Bottom navigation, bottom nav, dock

**Sidebar**:
A persistent vertical panel at the side of the app holding navigation or tools.[^hig-sidebars][^shadcn-sidebar]
_Avoid_: Navigation drawer, side nav, left menu

**Navigation rail**:
A narrow sidebar that shows only icons, with short labels or none.[^m3-nav-rail]
_Avoid_: Collapsed sidebar, icon bar

**Mega menu**:
A large navigation panel opened from a top-bar item that shows many links in groups.[^nng-mega-menu][^radix-navigation-menu]
_Avoid_: Dropdown navigation, flyout

**Hamburger menu**:
Navigation hidden behind a three-line icon that opens a sheet or full-screen menu.[^nng-hamburger]
_Avoid_: Burger, mobile menu (name the panel separately)

**Breadcrumb**:
A trail of links showing the current page's position in a hierarchy.[^apg-breadcrumb][^nng-breadcrumbs]
_Avoid_: Path, trail

**Pagination**:
Numbered page links that split a long list into pages.[^nng-infinite]
_Avoid_: Pager, paging

**Infinite scroll**:
Loading more items automatically as the user nears the end of a list.[^nng-infinite]
_Avoid_: Endless scroll, auto-load; use **Load more** for the button variant

**Scroll container**:
An element with its own scrolling (`overflow: auto`), separate from page scroll.[^mdn-overscroll]
_Avoid_: Scroll area (the styled component), scroller

**Scroll lock**:
Stopping the page behind a modal overlay from scrolling while the overlay is open.[^base-ui-drawer]
_Avoid_: Body freeze, no-scroll

**Scroll chaining**:
Scroll that passes to the outer page once a nested scroll container reaches its end; turned off with `overscroll-behavior: contain`.[^mdn-overscroll]
_Avoid_: Scroll leaking, scroll bleed

**Scroll snap**:
Scroll that comes to rest aligned to item edges, as in a swipeable row of cards.[^mdn-scroll-snap]
_Avoid_: Snap scrolling, paging scroll

**Scroll padding**:
Space reserved at the edge of a scroll container so that jumped-to or snapped content is not hidden under a sticky top bar.[^mdn-scroll-padding]
_Avoid_: Anchor offset, header offset hack

**Smooth scroll**:
Animated scrolling to a target instead of an instant jump.[^mdn-scroll-behavior]
_Avoid_: Animated scroll, scroll easing

**Scrollbar gutter**:
Space reserved for the scrollbar, so content does not shift sideways when a scrollbar appears.[^mdn-scrollbar-gutter]
_Avoid_: Scrollbar jump fix

**Scrolljacking**:
Taking over the native scroll speed or direction to drive custom effects.[^nng-scrolljacking]
_Avoid_: Custom scroll, scroll hijack

### Forms

**Field**:
One form unit: label, control, description and error message together.[^base-ui-list]
_Avoid_: Input (only the control), form row, form group

**Label**:
The visible text naming a control, programmatically tied to it.[^nng-placeholder]
_Avoid_: Caption, title

**Placeholder**:
Hint text inside an empty input that disappears on typing; it is never a substitute for a label.[^nng-placeholder]
_Avoid_: Hint text, ghost text, label

**Floating label**:
A label shown inside an empty input that moves above the input when it gets focus or a value.[^convention]
_Avoid_: Animated label, inset label

**Description**:
Helper text under a control that explains the expected input (`aria-describedby`).[^base-ui-list]
_Avoid_: Helper text, hint, sub-label

**Error message**:
Text tied to a field that says what is wrong with its value and how to fix it.[^nng-indicators][^nng-form-errors]
_Avoid_: Validation (that is the check), warning

**Inline validation**:
Checking a field and showing its error next to it while the user fills in the form, not only on submit.[^nng-form-errors]
_Avoid_: Live validation, instant validation

**Validation timing**:
When a field's error first appears (on blur, on submit, or while typing); `:user-invalid` matches only after the user has interacted.[^mdn-user-invalid]
_Avoid_: Validation mode, eager/lazy validation

**Error summary**:
A list of every error at the top of a form after a failed submit, each linking to its field.[^nng-form-errors]
_Avoid_: Form alert, error banner

**Required indicator**:
The mark (usually an asterisk) that tells which fields must be filled.[^nng-form-errors]
_Avoid_: Asterisk, mandatory flag

**Fieldset**:
A group of related controls under one caption (its legend), such as a radio group or an address block.[^base-ui-list]
_Avoid_: Form section, group box

**Input group**:
An input combined with attached prefix or suffix items such as an icon, a unit, or a button.[^shadcn-input-group]
_Avoid_: Input addon, adornment, affix

**OTP field**:
A row of single-character boxes for a one-time code that moves focus forward as digits are typed.[^base-ui-list]
_Avoid_: PIN input, code input, verification boxes

### Motion beyond `emilkowalski-animation-vocabulary`

**Starting style**:
The styles an element animates from when it first appears or leaves `display: none`, set with `@starting-style`.[^mdn-starting-style]
_Avoid_: Initial state, from-state

**View transition name**:
The name that pairs an element in the old view with one in the new view, so the view transition morphs between them.[^w3c-view-transitions]
_Avoid_: Shared element id, morph key

**View timeline**:
A scroll-driven animation timeline whose progress tracks one element moving through its scrollport, not total scroll position.[^mdn-scroll-driven]
_Avoid_: Scroll reveal (one-shot trigger), intersection animation

**Background indent**:
The page behind an open drawer scaling down and receding, as in iOS sheets.[^base-ui-drawer]
_Avoid_: Scale background, iOS sheet effect

**Motion path**:
A path that an element moves along, set with `offset-path`.[^mdn-offset-path]
_Avoid_: Path animation, follow path

**Layout shift**:
Visible content jumping position after first render because something above or around it changed size, such as a late image, a font swap or a banner.[^mdn-cls]
_Avoid_: Jump, content jank, CLS (the metric)

**Scroll anchoring**:
The browser keeping the visible content in place when content above it changes size (`overflow-anchor`).[^mdn-scroll-anchoring]
_Avoid_: Scroll jump fix

### Accessibility

**Accessible name**:
The text an assistive technology announces for an element, from its label, its content or `aria-label`.[^apg-button-name]
_Avoid_: Alt text (images only), screen-reader label

**Visually hidden**:
Content that screen readers read but sighted users do not see.[^wcag-c7]
_Avoid_: sr-only (class name), hidden (removes it for everyone)

**Skip link**:
A first-in-tab-order link that jumps past repeated navigation to the main content.[^wcag-bypass]
_Avoid_: Skip nav, jump link

**Landmark**:
A labelled page region (banner, navigation, main, complementary, contentinfo) that assistive technology can jump between.[^apg-landmarks]
_Avoid_: Section, region (generic)

**Focus trap**:
Keeping Tab inside an open modal overlay until it closes, and returning focus to the trigger after it closes.[^apg-dialog]
_Avoid_: Focus lock, focus loop

**Roving focus**:
In a composite widget (tabs, toolbar, listbox) only one item is in the Tab order and arrow keys move between items.[^apg-keyboard]
_Avoid_: Roving tabindex (the technique), arrow navigation

**Contrast ratio**:
The luminance ratio between text or a UI part and its background; WCAG AA needs 4.5:1 for body text, 3:1 for large text and for UI parts.[^wcag-contrast][^wcag-non-text]
_Avoid_: Readability, color contrast (when the number is meant)

**Target size**:
The clickable area of a control, which may extend beyond its visible shape.[^wcag-target]
_Avoid_: Hit area, tap area, touch target

[^apg-dialog]: APG Dialog (Modal): https://www.w3.org/WAI/ARIA/apg/patterns/dialog-modal/ (URL 200)
[^apg-listbox]: APG Listbox: https://www.w3.org/WAI/ARIA/apg/patterns/listbox/ (URL 200)
[^apg-disclosure]: APG Disclosure: https://www.w3.org/WAI/ARIA/apg/patterns/disclosure/ (read)
[^apg-tabs]: APG Tabs: https://www.w3.org/WAI/ARIA/apg/patterns/tabs/ (URL 200)
[^apg-breadcrumb]: APG Breadcrumb: https://www.w3.org/WAI/ARIA/apg/patterns/breadcrumb/ (URL 200)
[^apg-keyboard]: APG Developing a Keyboard Interface: https://www.w3.org/WAI/ARIA/apg/practices/keyboard-interface/ (URL 200)
[^apg-landmarks]: APG Landmark Regions: https://www.w3.org/WAI/ARIA/apg/practices/landmark-regions/ (URL 200)
[^apg-button-name]: APG Button pattern (accessible name), listed on the patterns index: https://www.w3.org/WAI/ARIA/apg/patterns/ (read)
[^wcag-hover-focus]: WCAG 2.2 Understanding 1.4.13 Content on Hover or Focus: https://www.w3.org/WAI/WCAG22/Understanding/content-on-hover-or-focus.html (read)
[^wcag-contrast]: WCAG 2.2 Understanding 1.4.3 Contrast (Minimum): https://www.w3.org/WAI/WCAG22/Understanding/contrast-minimum.html (URL 200)
[^wcag-non-text]: WCAG 2.2 Understanding 1.4.11 Non-text Contrast: https://www.w3.org/WAI/WCAG22/Understanding/non-text-contrast.html (URL 200)
[^wcag-target]: WCAG 2.2 Understanding 2.5.8 Target Size (Minimum): https://www.w3.org/WAI/WCAG22/Understanding/target-size-minimum.html (URL 200)
[^wcag-bypass]: WCAG 2.2 Understanding 2.4.1 Bypass Blocks: https://www.w3.org/WAI/WCAG22/Understanding/bypass-blocks.html (URL 200)
[^w3c-view-transitions]: CSS View Transitions Module Level 1: https://www.w3.org/TR/css-view-transitions-1/ (URL 200)
[^mdn-media-hover]: MDN `hover` media feature, via the `/Web/CSS/@media/hover` path that redirects: https://developer.mozilla.org/en-US/docs/Web/CSS/@media/hover (URL 200)
[^mdn-focus-visible]: MDN `:focus-visible`: https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Selectors/:focus-visible (URL 200)
[^mdn-user-invalid]: MDN `:user-invalid`: https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Selectors/:user-invalid (URL 200)
[^mdn-disabled]: MDN `disabled` attribute: https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Attributes/disabled (URL 200)
[^mdn-readonly]: MDN `readonly` attribute: https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Attributes/readonly (URL 200)
[^mdn-aria-disabled]: MDN `aria-disabled`: https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/Reference/Attributes/aria-disabled (URL 200)
[^mdn-overscroll]: MDN `overscroll-behavior`, scroll chaining: https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Properties/overscroll-behavior (read)
[^mdn-scroll-snap]: MDN Scroll snap: https://developer.mozilla.org/en-US/docs/Web/CSS/Guides/Scroll_snap (URL 200)
[^mdn-scroll-padding]: MDN `scroll-padding`: https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Properties/scroll-padding (URL 200)
[^mdn-scroll-behavior]: MDN `scroll-behavior`: https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Properties/scroll-behavior (URL 200)
[^mdn-scrollbar-gutter]: MDN `scrollbar-gutter`: https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Properties/scrollbar-gutter (URL 200)
[^mdn-starting-style]: MDN `@starting-style`: https://developer.mozilla.org/en-US/docs/Web/CSS/@starting-style (URL 200)
[^mdn-scroll-driven]: MDN Scroll-driven animations: https://developer.mozilla.org/en-US/docs/Web/CSS/Guides/Scroll-driven_animations (URL 200)
[^radix-navigation-menu]: Radix Navigation Menu: https://www.radix-ui.com/primitives/docs/components/navigation-menu (URL 200)
[^base-ui-list]: Base UI component list (Field, Fieldset, Number Field, OTP Field, Toggle, Separator, Scroll Area, Avatar, Select, Slider): https://base-ui.com/react/overview/quick-start (read)
[^base-ui-preview-card]: Base UI Preview Card, opens on hover or focus after a delay: https://base-ui.com/react/components/preview-card (read)
[^base-ui-drawer]: Base UI Drawer (swipe, snap points, indent, modal by default): https://base-ui.com/react/components/drawer (read)
[^shadcn-skeleton]: shadcn Skeleton: https://ui.shadcn.com/docs/components/base/skeleton (URL 200)
[^shadcn-empty]: shadcn Empty: https://ui.shadcn.com/docs/components/base/empty (URL 200)
[^shadcn-input-group]: shadcn Input Group: https://ui.shadcn.com/docs/components/base/input-group (URL 200)
[^shadcn-sidebar]: shadcn Sidebar: https://ui.shadcn.com/docs/components/base/sidebar (URL 200)
[^react-use-optimistic]: React `useOptimistic`: https://react.dev/reference/react/useOptimistic (URL 200)
[^hig-progress]: Apple HIG Progress indicators, determinate and indeterminate: https://developer.apple.com/design/human-interface-guidelines/progress-indicators (read)
[^hig-tab-bars]: Apple HIG Tab bars: https://developer.apple.com/design/human-interface-guidelines/tab-bars (JSON 200, not read)
[^hig-sidebars]: Apple HIG Sidebars: https://developer.apple.com/design/human-interface-guidelines/sidebars (JSON 200, not read)
[^m3-state-layer]: M3 States: state layers: https://m3.material.io/foundations/interaction/states/state-layers (search summary only; the page renders only with JavaScript)
[^m3-nav-rail]: M3 Navigation rail: https://m3.material.io/components/navigation-rail/overview (URL 200, not readable)
[^nng-indicators]: NN/g Indicators, validations and notifications (toast): https://www.nngroup.com/articles/indicators-validations-notifications/ (read)
[^nng-skeleton]: NN/g Skeleton screens compared with spinners and progress bars: https://www.nngroup.com/articles/skeleton-screens/ (read)
[^nng-empty]: NN/g Empty states: https://www.nngroup.com/articles/empty-state-interface-design/ (URL 200)
[^nng-form-errors]: NN/g Error messages in forms: https://www.nngroup.com/articles/errors-forms-design-guidelines/ (URL 200)
[^nng-placeholder]: NN/g Placeholders in form fields: https://www.nngroup.com/articles/form-design-placeholders/ (URL 200)
[^nng-mega-menu]: NN/g Mega menus: https://www.nngroup.com/articles/mega-menus-work-well/ (URL 200)
[^nng-hamburger]: NN/g Hamburger menus: https://www.nngroup.com/articles/hamburger-menus/ (URL 200)
[^nng-breadcrumbs]: NN/g Breadcrumbs: https://www.nngroup.com/articles/breadcrumbs/ (URL 200)
[^nng-infinite]: NN/g Infinite scrolling compared with pagination: https://www.nngroup.com/articles/infinite-scrolling-tips/ (URL 200)
[^nng-scrolljacking]: NN/g Scrolljacking: https://www.nngroup.com/articles/scrolljacking-101/ (URL 200)
[^mdn-offset-path]: MDN `offset-path`: https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Properties/offset-path (URL 200)
[^mdn-cls]: MDN Glossary, Cumulative Layout Shift: https://developer.mozilla.org/en-US/docs/Glossary/CLS (URL 200)
[^mdn-scroll-anchoring]: MDN Scroll anchoring: https://developer.mozilla.org/en-US/docs/Web/CSS/Guides/Scroll_anchoring/Overview (URL 200)
[^wcag-c7]: WCAG Technique C7, Using CSS to hide a portion of the link text: https://www.w3.org/WAI/WCAG22/Techniques/css/C7 (title read)
[^convention]: None of the primary sources consulted names this concept; the name comes from common practice, and the owner chose it on 2026-10-28.
