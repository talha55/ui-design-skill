# Step 3: Build

Build the agreed direction. Nothing in this step is a new design decision; if you find yourself changing the palette or the structure, go back to the direction and say so.

## Mobile first

Write the narrow layout first, then add wider breakpoints. Most visitors to a local business arrive on a phone, often in a hurry.

- At 390 px wide nothing scrolls sideways and nothing overlaps.
- The primary action is reachable without scrolling. For a business people phone, the number is a tappable `tel:` link in the header.
- Tap targets are at least 44 px tall.

## Spacing

Use one scale and nothing outside it: 4, 8, 12, 16, 24, 32, 48, 64, 96, 128 px.

- Space inside a component is smaller than the space between components, which is smaller than the space between sections. This is what makes groups readable.
- Related things sit close together. A heading is closer to the text it introduces than to the text above it.
- Section padding is generous and consistent in feel, not identical in number: a dense section can be tighter, a hero or a closing call to action can breathe more.

## Type scale

Pick one scale and use only its steps. A workable one for text and ordinary headings: 14, 16, 18, 20, 24, 30, 36, 48, 60, 72 px. Display headings go far beyond it: size the hero headline and the closing line with `clamp()` so they reach 10 to 16 percent of the viewport width on a wide screen and still fit on a phone, for example `font-size: clamp(2.75rem, 11vw, 11rem)`.

- Body text is 16 to 18 px with a line height near 1.6.
- Headings have a tight line height, 0.9 to 1.1 at display sizes, and negative letter spacing (around -0.03em) at large sizes.
- Lines of body text run 45 to 75 characters. Set a max width on text blocks; never let a paragraph span a wide screen.
- Use size and weight to show importance. A page should have one largest thing, a few medium things and a lot of quiet text.
- Left-align body text. Centre only short headings and short calls to action.

## Layout

- Use a 12 column grid for content, with side gutters of at least 16 px on mobile. Do not trap the whole page inside a narrow centred column: let images, colour blocks, display type and scenes run the full width of the screen.
- Overlap things. An image that crosses a section boundary, a heading that sits partly over a photo, a label at an angle. Layers give depth; boxes stacked in a column do not.
- Do not centre everything. Left-aligned content with a clear edge reads as designed; a page of centred blocks reads as a template.
- Vary the sections. Alternate between a split layout, a full-width band, a grid, a list. Two neighbouring sections should not have the same shape.
- Break symmetry on purpose somewhere: an image that runs to the edge, an offset column, a list that is not a row of equal cards.

## Hero

- One message: what the business does and for whom, in the visitor's words. Add where, when the business is local.
- One primary action, visibly a button, in the accent colour. At most one secondary action, visibly quieter.
- The first screen is a statement that fills the viewport: a full-bleed photograph or video with type over it, a headline so large it is the image, or a living colour field. Not a headline, a paragraph and two buttons on a plain background.
- Do not stack badges, ratings or counters under the headline unless they were supplied.

## Sections

- Services are not automatically three icon cards. Six services might be a two column list with a line each, a set of rows with an image, or a featured service beside a compact list. Choose by content.
- Every section has one job. If you cannot say what a section is for in five words, cut it.
- Reuse the primary action after long sections and at the end of the page.

## Components

- **Buttons:** one primary style, one secondary, one text link. The primary has the accent background and enough padding to look pressable. Label them with the action and, for a call button, the number itself.
- **Cards:** use a card only when the content is a separate object. Do not put cards inside cards. Either a border or a shadow, not both.
- **Forms:** visible labels above fields, not placeholder-only. Ask for the fewest fields that make the request useful. Say what happens after sending.
- **Navigation:** the business name, three to five links at most, and the primary action. On mobile keep the action visible and fold the links away.
- **Footer:** contact details, hours, service area, and nothing invented.

## Atmosphere

- No section is a flat white or flat grey rectangle by default. Give backgrounds something: a photograph, a full colour block, a gradient with grain, a texture, a large cropped letterform or number behind the content.
- Change the background between sections so the page has chapters: dark to light, colour to photograph. A page that is one background from top to bottom has no rhythm.
- Use large numbers, labels and thin rules as design elements.

## Consistency

- One corner radius for small elements and one for large surfaces.
- At most two shadow levels. Shadows are soft and slightly tinted, never hard black. In the dark and vivid signature, glow in the accent colour replaces shadow.
- Borders are one pixel in a neutral from the palette.
- Every colour on the page is one of the palette's named colours.

## Content

Use the brief's facts and plain words. Write the way the owner would say it to a neighbour. No slogans that could describe any business ("quality you can trust", "excellence in every detail"). Where a fact is missing, leave a clearly labelled placeholder rather than writing around it.
