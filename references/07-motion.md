# Step 7: Motion

Animation should make the page feel responsive and guide the eye once. It should never make a visitor wait, and it should never be the first thing they notice.

## The library

Use Motion (`motion.dev`). It was formerly called Framer Motion; it is the same library under its current name.

Plain HTML:

```html
<script type="module">
  import { animate, inView, stagger } from "https://cdn.jsdelivr.net/npm/motion@latest/+esm";

  const reduce = window.matchMedia("(prefers-reduced-motion: reduce)").matches;
  if (!reduce) {
    inView("[data-reveal]", (element) => {
      animate(element, { opacity: [0, 1], y: [16, 0] }, { duration: 0.5, ease: "easeOut" });
    }, { amount: 0.25 });
  }
</script>
```

React or Next.js:

```jsx
import { motion, useReducedMotion } from "motion/react";
```

For a published site, pin the major version instead of `latest`.

## How much

Use the level agreed in the direction.

- **Low:** hover and press feedback on interactive elements. Nothing else moves.
- **Medium:** low, plus each section's content fades and rises into place once as it enters the screen.
- **High:** medium, plus a short hero sequence on load and one or two scroll-linked accents, such as an image that shifts slightly as the page scrolls.

Most business sites should be low or medium. High is for brands where the feel of the site is part of the product.

## Timing

- Feedback (hover, press, toggles): 120 to 200 ms.
- Entrances: 300 to 600 ms.
- Nothing longer than 800 ms unless it is a deliberate hero moment.
- Entrances ease out: fast start, gentle stop. Exits ease in. Avoid linear timing and avoid bounce on a business site.
- Stagger groups by 40 to 80 ms per item, and cap the total: a list of twelve items should not take a second to finish appearing.

## What to animate

- Animate only `transform` and `opacity`. Animating width, height, margin or top and left causes stutter.
- Small distances: 8 to 24 px of travel, scale between 0.97 and 1.03. Large movements look cheap.
- An entrance plays once. Do not replay it every time the element scrolls back into view.
- Hover: a small lift, a shade change, an arrow that moves a few pixels.
- Press: a slight scale down, around 0.98.

## What not to animate

- The primary action and the headline are visible and usable on first paint. Do not hide them behind an entrance animation; a visitor in a hurry should be able to tap "Call" at once.
- No animation that blocks reading: no text typed out letter by letter, no counters ticking up to numbers, no content that waits for a scroll position to become legible.
- No continuous motion in the background: floating shapes, pulsing buttons, endless marquees. The one exception is a quiet background video in the hero.
- Nothing that shifts the layout while it loads.
- No scroll hijacking. The page scrolls at the speed the visitor chooses.

## Reduced motion

Some people set their device to reduce motion because movement makes them unwell. Respect it always.

- Check `prefers-reduced-motion: reduce` (in React, `useReducedMotion()`).
- When it is set: no entrances, no scroll-linked effects, no autoplaying video. Content is simply present. Colour and opacity changes on hover may stay.
- Elements that start hidden for an entrance must be visible by default when motion is reduced or when the script fails to load. Set the hidden starting state from the script, not in the CSS, so a failed script never leaves the page blank.
