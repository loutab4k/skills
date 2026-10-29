# UI vocabulary: layout, type and color

Canonical names for how a screen is laid out, set in type and colored, so a request for a UI change names one concept precisely. The other UI files: [ui-components.md](ui-components.md), [ui-interaction.md](ui-interaction.md). Motion terms live in `emilkowalski-animation-vocabulary`; [ui-interaction.md](ui-interaction.md) adds only the motion terms missing there. Where a term shares a name with one of its motion terms (Skeleton, Accordion), the entry here names the element or state and the motion stays there.

## Language

### Layout and spacing

**Viewport**:
The visible area of the page in the browser window; on mobile its height changes as the browser bars show and hide.[^mdn-length]
_Avoid_: Screen, window

**Dynamic viewport height**:
The `dvh` unit, which tracks the viewport as mobile browser bars expand and retract; `svh` is the height with bars shown, `lvh` the height with bars hidden.[^mdn-length]
_Avoid_: 100vh fix, full-screen height

**Safe area**:
The part of the screen not covered by a notch, rounded corners, home indicator or status bar, read in CSS through `env(safe-area-inset-*)`.[^hig-layout][^mdn-env]
_Avoid_: Notch padding, unsafe zone

**Breakpoint**:
A viewport width at which the layout switches to a different arrangement.[^mdn-container-queries]
_Avoid_: Media size, screen size

**Container query**:
A style rule that responds to the size of an element's container rather than to the viewport.[^mdn-container-queries]
_Avoid_: Element query

**Fluid size**:
A size that scales continuously between a minimum and maximum with the viewport or container, typically written with `clamp()`.[^mdn-clamp]
_Avoid_: Responsive size, auto-scaling font

**Content width**:
The maximum width of the centered column that holds a page's content.[^convention]
_Avoid_: Container (clashes with container query), wrapper, max-width box

**Full-bleed**:
An element that breaks out of the content width to span the full viewport width.[^convention]
_Avoid_: Edge-to-edge, breakout (as a noun)

**Gutter**:
The fixed space between grid columns, and the space between content and the viewport edge.[^mdn-gap]
_Avoid_: Margin (for column spacing)

**Gap**:
The space between sibling items in a flex or grid layout, set on the parent and never on the children.[^mdn-gap]
_Avoid_: Spacing between, margin-between

**Inset**:
The distance between a positioned element and the edges of its containing block, or between content and the inner edge of its box.[^mdn-logical]
_Avoid_: Offset, top/left (when direction-neutral is meant)

**Inline axis**:
The direction text runs in a line (horizontal in English); the block axis is the direction in which lines stack. Logical properties use `inline-start`/`inline-end` instead of left/right.[^mdn-logical]
_Avoid_: Horizontal, left/right (in RTL-aware code)

**Spacing scale**:
The fixed set of spacing steps (for example 4, 8, 16, 24, 40) that every margin, padding and gap must use.[^convention]
_Avoid_: Magic numbers, arbitrary spacing

**Density**:
How tightly content is packed: how much padding, line height and gap surround each item.[^convention]
_Avoid_: Compactness, tightness

**Visual hierarchy**:
The order in which the eye reads elements, produced by size, weight, color, contrast and position.[^nng-hierarchy]
_Avoid_: Emphasis order, importance

**Whitespace**:
Empty space around and between elements that groups related items and separates unrelated ones.[^hig-layout]
_Avoid_: Negative space (use only for art-direction talk), empty area

**Aspect ratio**:
The fixed width-to-height proportion of a box, kept as its width changes.[^mdn-aspect-ratio]
_Avoid_: Proportions, image ratio

**Object fit**:
How an image or video fills its box: `cover` crops to fill, `contain` letterboxes to show all.[^mdn-object-fit]
_Avoid_: Image scaling, background-size (for `<img>`)

**Sticky**:
An element that scrolls normally until it reaches an edge of its scroll container and then stays pinned there; unlike Fixed, it stays inside its parent.[^mdn-position]
_Avoid_: Fixed (when sticky is meant), pinned header (ambiguous)

**Stacking context**:
A group of elements whose `z-index` values compete only with each other; a child can never rise above an element outside its stacking context.[^mdn-position]
_Avoid_: Z-index layer, z-order

### Typography

**Type scale**:
The fixed set of text styles (size, weight, line height) a product uses, named by role: display, headline, title, body, label.[^m3-type]
_Avoid_: Font sizes, heading sizes

**Text role**:
The job a text style does: display (hero numbers and short headlines), headline, title, body, label (UI controls), caption.[^m3-type]
_Avoid_: H1-style, big text

**Eyebrow**:
A short, small, often uppercase label set above a heading to name its section or category.[^convention]
_Avoid_: Overline, kicker, pre-title

**Line height**:
The vertical distance from one baseline of text to the next.[^mdn-line-height]
_Avoid_: Leading (Apple also uses "leading" for the start side), line spacing

**Letter spacing**:
Uniform extra space added between all characters in a run of text.[^mdn-letter-spacing][^hig-typography]
_Avoid_: Tracking, character spacing

**Kerning**:
Spacing adjustments between specific letter pairs, built into the font.[^mdn-kerning]
_Avoid_: Letter spacing (different thing)

**Measure**:
The length of a line of text, usually counted in characters.[^wcag-visual]
_Avoid_: Line length, text width, column width

**Balanced wrap**:
Wrapping a short block (a heading) so its lines come out roughly equal in length, via `text-wrap: balance`.[^mdn-text-wrap]
_Avoid_: Even lines, heading wrap

**Pretty wrap**:
Wrapping body text with a slower algorithm that avoids a lone short word on the last line, via `text-wrap: pretty`.[^mdn-text-wrap]
_Avoid_: Orphan control (CSS `orphans` means something else)

**Runt**:
A single short word left alone on the last line of a paragraph or heading.[^mdn-text-wrap]
_Avoid_: Orphan, widow (both contested)

**Truncation**:
Cutting overflowing single-line text and ending it with an ellipsis, via `text-overflow: ellipsis`.[^mdn-text-overflow]
_Avoid_: Clipping, dot-dot-dot

**Line clamp**:
Limiting multi-line text to N lines with an ellipsis on the last one.[^mdn-line-clamp]
_Avoid_: Multi-line truncation, max lines

**Optical size**:
A variable-font axis that redraws glyphs for small or large sizes, with sturdier small text and finer display text.[^mdn-optical-sizing]
_Avoid_: Font scaling

**Leading trim**:
Removing the empty space above cap height and below the baseline of a text box so it aligns tightly with neighbours, via `text-box`.[^mdn-text-box-trim]
_Avoid_: Text-box crop, half-leading hack

**Cap height**:
The height of capital letters above the baseline; x-height is the height of lowercase letters.[^mdn-text-box-trim]
_Avoid_: Letter height

**Hanging punctuation**:
Placing opening quotes or bullets outside the text's left edge so the letters themselves align.[^mdn-hanging-punctuation]
_Avoid_: Outdented quote

**FOUT**:
A flash of the fallback font before the web font loads and swaps in, controlled by `font-display`.[^mdn-font-display]
_Avoid_: Font flicker, font jump

**Underline offset**:
The distance between the text baseline and its underline, set with `text-underline-offset`.[^mdn-underline-offset]
_Avoid_: Link underline spacing

### Color and surface

**Color token**:
A named color variable; a semantic token (`danger`, `surface`) names a role and points to a primitive token (`red-600`) that names a value.[^material-web-color]
_Avoid_: Color variable, palette color (when a role is meant)

**Surface**:
The background color of an area that holds content; a product has a few surface levels for nesting.[^material-web-color][^m3-tonal-blog]
_Avoid_: Background (reserve for the page itself), panel color

**Surface level**:
One step in a ladder of surface colors (lowest to highest container), used to show nesting and elevation without shadows.[^m3-tonal-blog]
_Avoid_: Tonal elevation level, surface tint

**Elevation**:
How far a layer appears above the page, expressed by a shadow, a surface level, or both.[^m3-tonal-blog][^mdn-box-shadow]
_Avoid_: Depth, z-height, shadow (shadow is one way to express it)

**Shadow**:
A drop shadow under an element (`box-shadow`); layered shadows mix a tight dark shadow with a wide soft one.[^mdn-box-shadow]
_Avoid_: Glow, elevation (when only the shadow is meant)

**Material**:
A translucent background that blurs and tints what is behind it, via `backdrop-filter`.[^hig-materials][^mdn-backdrop-filter]
_Avoid_: Glassmorphism, frosted glass, blur background

**Backdrop**:
The full-screen layer behind a modal overlay that dims or blurs the page (CSS `::backdrop`; Base UI `Backdrop`).[^mdn-backdrop][^nng-bottom-sheet]
_Avoid_: Scrim, overlay (Radix/shadcn part name), dimmer

**On-color**:
The foreground color (text, icon) meant to sit on a given surface or fill, such as on-primary on a primary button.[^material-web-color]
_Avoid_: Text color on X, contrast color

**Accent color**:
The brand color used for primary actions, selection and focus; in CSS `accent-color` tints native checkboxes, radios and range inputs.[^mdn-accent-color]
_Avoid_: Brand color (when the role is meant), highlight

**Destructive color**:
The semantic color for actions that delete or lose data, distinct from the error color for invalid input.[^convention]
_Avoid_: Red, danger (when the action is meant), error color

**Border**:
The line drawn on the edge of a box that takes up layout space.[^material-web-color]
_Avoid_: Stroke, outline (CSS outline is different)

**Divider**:
A thin line between items or sections that separates content; ARIA and Radix/Base UI call it Separator.[^base-ui-list]
_Avoid_: Hairline, rule, horizontal line

**Ring**:
An outline drawn around an element outside its border without taking layout space (CSS `outline` plus `outline-offset`), used mainly for focus.[^mdn-outline-offset]
_Avoid_: Border (takes space), glow

**Color scheme**:
The light or dark mode the page renders in, declared with `color-scheme` and detected with `prefers-color-scheme`.[^mdn-color-scheme]
_Avoid_: Theme (themes can differ in more than lightness), night mode

**State layer**:
A translucent overlay in the content color that a control shows on hover, focus, press or drag, so every state reads the same on any fill.[^m3-state-layer]
_Avoid_: Hover tint, highlight overlay

[^mdn-length]: MDN `<length>`, viewport units: https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Values/length (read)
[^mdn-env]: MDN `env()`: https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Values/env (URL 200)
[^mdn-container-queries]: MDN Container queries: https://developer.mozilla.org/en-US/docs/Web/CSS/Guides/Containment/Container_queries (URL 200)
[^mdn-clamp]: MDN `clamp()`: https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Values/clamp (URL 200)
[^mdn-gap]: MDN `gap`: https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Properties/gap (URL 200)
[^mdn-logical]: MDN Logical properties and values: https://developer.mozilla.org/en-US/docs/Web/CSS/Guides/Logical_properties_and_values (URL 200)
[^mdn-aspect-ratio]: MDN `aspect-ratio`: https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Properties/aspect-ratio (URL 200)
[^mdn-object-fit]: MDN `object-fit`: https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Properties/object-fit (URL 200)
[^mdn-position]: MDN `position`: https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Properties/position (URL 200)
[^mdn-line-height]: MDN `line-height`: https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Properties/line-height (URL 200)
[^mdn-letter-spacing]: MDN `letter-spacing`: https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Properties/letter-spacing (URL 200)
[^mdn-kerning]: MDN `font-kerning`: https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Properties/font-kerning (URL 200)
[^mdn-text-wrap]: MDN `text-wrap` (`balance`, `pretty`): https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Properties/text-wrap (read)
[^mdn-text-overflow]: MDN `text-overflow`: https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Properties/text-overflow (URL 200)
[^mdn-line-clamp]: MDN `line-clamp`: https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Properties/line-clamp (URL 200)
[^mdn-optical-sizing]: MDN `font-optical-sizing`: https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Properties/font-optical-sizing (URL 200)
[^mdn-text-box-trim]: MDN `text-box-trim`, Baseline 2026 newly available per the page: https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Properties/text-box-trim (read)
[^mdn-hanging-punctuation]: MDN `hanging-punctuation`: https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Properties/hanging-punctuation (URL 200)
[^mdn-font-display]: MDN `font-display`, via the `/Web/CSS/@font-face/font-display` path that redirects: https://developer.mozilla.org/en-US/docs/Web/CSS/@font-face/font-display (URL 200)
[^mdn-underline-offset]: MDN `text-underline-offset`: https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Properties/text-underline-offset (URL 200)
[^mdn-box-shadow]: MDN `box-shadow`: https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Properties/box-shadow (URL 200)
[^mdn-backdrop-filter]: MDN `backdrop-filter`: https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Properties/backdrop-filter (URL 200)
[^mdn-backdrop]: MDN `::backdrop`: https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Selectors/::backdrop (URL 200)
[^mdn-accent-color]: MDN `accent-color`: https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Properties/accent-color (URL 200)
[^mdn-outline-offset]: MDN `outline-offset`: https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Properties/outline-offset (URL 200)
[^mdn-color-scheme]: MDN `color-scheme`: https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Properties/color-scheme (URL 200)
[^base-ui-list]: Base UI component list (Field, Fieldset, Number Field, OTP Field, Toggle, Separator, Scroll Area, Avatar, Select, Slider): https://base-ui.com/react/overview/quick-start (read)
[^hig-layout]: Apple HIG Layout (safe areas, alignment, grouping): https://developer.apple.com/design/human-interface-guidelines/layout (read)
[^hig-typography]: Apple HIG Typography (tracking, Dynamic Type): https://developer.apple.com/design/human-interface-guidelines/typography (read)
[^hig-materials]: Apple HIG Materials: https://developer.apple.com/design/human-interface-guidelines/materials (read)
[^material-web-color]: Material Web color tokens (surface, surface-container-*, outline, outline-variant, on-*): https://github.com/material-components/material-web/blob/main/docs/theming/color.md (read)
[^m3-tonal-blog]: M3 blog "Introducing tone-based surfaces", surface roles decoupled from elevation: https://m3.material.io/blog/tone-based-surface-color-m3 (search summary only)
[^m3-state-layer]: M3 States: state layers: https://m3.material.io/foundations/interaction/states/state-layers (search summary only; the page renders only with JavaScript)
[^m3-type]: M3 type scale tokens (display, headline, title, body, label): https://m3.material.io/styles/typography/type-scale-tokens (URL 200, not readable; role names from knowledge of M3)
[^nng-bottom-sheet]: NN/g Bottom sheets (modal, nonmodal, grabber, scrim): https://www.nngroup.com/articles/bottom-sheet/ (read)
[^nng-hierarchy]: NN/g Visual hierarchy: https://www.nngroup.com/articles/visual-hierarchy-ux-definition/ (URL 200)
[^wcag-visual]: WCAG 2.2 Understanding 1.4.8 Visual Presentation (line length): https://www.w3.org/WAI/WCAG22/Understanding/visual-presentation.html (URL 200)
[^convention]: None of the primary sources consulted names this concept; the name comes from common practice, and the owner chose it on 2026-10-28.
