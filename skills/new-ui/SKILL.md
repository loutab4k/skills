---
name: new-ui
description: Design the UI of a new product, or redesign a page, site or screen, together with the owner, through a live demo, references and one signature move. Use when the owner asks for a new UI, a redesign, a pitch mock-up, or says a design is bland or ugly.
---

# New UI

A page wins when it reads as **one picture**: one idea carried by one signature move, shaped live by the owner's remarks. Cleaning up a template by the brief gives a tidy page with no idea, and the owner rejects it. Follow these steps in order; read `BINDINGS.md` beside this file first when it exists, for the host's taste file, kept prototypes, preview and guide paths.

## 1. Read the taste

Read the owner's taste file and kept prototypes, the project's design doc and brief, and the owner's remarks on earlier versions. Use the owner's words as the source of taste.

Done when you can name every owner rule that binds this page (fonts, colours, header, radii, motion speed) with its source.

## 2. Get references

Ask the owner for 2–4 recordings or sites whose presentation they like. From each, take the technique (how information is staged, how a header reacts, how motion lands) and rebuild it in this project's own style.

When the owner has none, build three contrasting versions of the first screen on one page and let the owner pick.

Done when the owner gave references or picked a version.

## 3. Choose the signature move

Propose one signature move drawn from the product's or client's own identity (what the product does, its mark, a shape from its sign, its material or photos) that recurs through the whole page: it draws in on load, leads to the main action, accents hover, joins sections and carries the header too. Offer it with two alternatives, each in one plain sentence, and recommend one.

Done when the owner chose one.

## 4. Build in a live loop

Build the page from scratch around the signature move, keeping the facts, palette and fonts. Keep the page open in a preview the owner watches. Show the first screen as soon as it stands, then work in a tight loop: the owner names an edit, you make it at once as a local change, and you report in one line what changed. Commit and open a PR only when the owner says so.

Done when the owner says the page is ready.

## 5. Move with physics

- Large objects move slower than small ones; a press answers at once.
- Load is choreography: lines or the signature move draw first, then objects arrive, then text lands briefly.
- Interaction motion follows the pointer or a spring; an object at rest stays still.
- A pointer interaction starts on the first event, also when the pointer already rests over the element after load or a scroll.
- The header changes tone crisply and smoothly as it passes over light and dark bands.
- Animate only composite properties (`transform`, `opacity`), and measure frame rate in each browser the owner uses: speed is part of every change, and the page keeps its sense of motion after it.

Use the host's motion and design skills to build and review each animation, and the host's web-platform guides for the technique.

## 6. Check before each showing

- Content stays within its edges: nothing stretches past the content width at the top, bottom or sides.
- The visual centre of each screen sits where the eye expects it.
- Every accent keeps contrast on each background it crosses.
- Every fact, name, number and price comes from the client; a missing one is left out.
- The page holds at 320, 375 and 1440 px, in light and dark.

## 7. Record verdicts

Write each keep or drop the owner gives into the taste file, in the owner's words, with the reason.

Done when every verdict of this session is in the taste file.
