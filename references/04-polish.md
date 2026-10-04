# Step 4: Polish

A second pass, after the page is built. Nothing structural changes here. You are looking for the small things that separate a finished page from a first draft. Go through the page top to bottom once for each heading below.

## Alignment

- Every element's left edge lines up with something. Count the distinct left edges in a section: more than two or three means something is drifting.
- Text baselines in a row line up. Icons sit on the text's centre line, not above it.
- Images in a row share a height and an aspect ratio.

## Rhythm

- Read the vertical gaps down the page. They should come from the spacing scale and group related things. Fix any gap that is "almost" the same as its neighbour.
- A heading sits closer to its own content than to the section above.
- Lists and grids have the same gap between every item.

## States

Every link, button and field needs all of these, and each must be visible:

- **Hover:** a clear change, such as a darker shade or a small lift.
- **Focus:** a visible outline for keyboard users, using `:focus-visible`, at least 2 px, with enough contrast against the background. Never remove the outline without replacing it.
- **Active:** a pressed look.
- **Disabled and error**, for form fields, with the error explained in words, not only in colour.

## Contrast

Check the real colours as used, including:

- Text over photos and video. Add an overlay or move the text; do not rely on the photo being dark.
- Muted text on tinted backgrounds.
- Text on the accent colour.
- Placeholder text and borders of form fields.

Body text needs 4.5:1, large text and interface elements 3:1.

## Content extremes

- What happens when a heading is twice as long? When a service name wraps to three lines? Fix layouts that only work with the sample text.
- No single word alone on the last line of a heading where it can be avoided.
- No paragraph wider than about 75 characters.

## Narrow screens

Look at 390 px again after all changes:

- No sideways scroll.
- No text smaller than 14 px.
- Tap targets at least 44 px tall with space between them.
- The primary action is still reachable without scrolling.

## Small details

- Phone numbers are `tel:` links and email addresses are `mailto:` links.
- The page has a real `<title>`, a meta description, and a language attribute.
- Headings are in order: one `h1`, then `h2` for sections.
- Images have width and height set so the page does not jump while loading.
- Nothing on the page is a default: no default blue links, no unstyled form controls, no default list bullets where a designed list is meant.
