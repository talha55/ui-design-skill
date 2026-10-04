# Step 7: Motion

Motion is what makes a visitor say "wow", and it is also what makes a page feel cheap when it is done without thought. The difference is choreography: a few well-built moments, each with a reason, instead of everything fading up the same way.

Working code for every move named here is in `references/motion-patterns.md`. Read it now and copy from it; do not write these patterns from memory.

## The library

Use Motion (`motion.dev`), formerly called Framer Motion. For smooth scrolling on a page with scroll-driven scenes, add Lenis. Both load from a CDN for a standalone page; in React use `motion/react`.

## Choreography

Plan the motion as a sequence before writing any of it.

1. **The opening.** What happens in the first two seconds. Usually the headline rising line by line, then the supporting pieces a beat later, then the image or video settling in. One orchestrated sequence, not five separate fades.
2. **The scroll story.** How each section arrives. Vary it: one section's image wipes open, the next holds still while its content changes, the next slides sideways. Two sections in a row should not arrive the same way.
3. **The centrepiece.** At least one scroll-driven scene on a page at the full level: a pinned section where an image grows to fill the screen, a horizontal gallery, or a sequence of statements that replace each other.
4. **The touch.** What responds to the pointer: buttons that lean towards it, cards that tilt, links whose underline draws in, a cursor that grows over things you can click.
5. **The ending.** The last screen deserves a moment too: a very large closing line, a final call to action that arrives with weight.

## Levels

Use the level agreed in the direction.

- **Full.** The default. All five parts of the choreography. At least three distinct moments, one of them scroll-driven. Smooth scrolling on.
- **Medium.** The opening, varied section reveals and pointer feedback. No pinned scenes.
- **Quiet.** Hover and press feedback and one gentle opening. For requests that ask for simple or minimal, and for visitors who are in a hurry.

## Which moves suit which signature

- **Cinematic scroll:** pinned scenes, an image growing to full screen, parallax on large images, lines of text appearing one at a time, a horizontal gallery, smooth scrolling.
- **Bold editorial:** a headline rising line by line, images revealed by a wipe, sharp quick timing, a background that changes colour between sections, underlines that draw in.
- **Dark and vivid:** a living gradient behind the hero, grain, cards that tilt towards the pointer, borders and glows that respond to hover, a cursor follower.
- **Playful and kinetic:** marquee bands, magnetic buttons, springy hovers with overshoot, elements that rotate into place, a cursor follower.

## Timing

- Feedback (hover, press): 120 to 250 ms.
- Reveals: 600 to 1100 ms with a long, soft landing. The ease `[0.16, 1, 0.3, 1]` suits almost everything.
- Stagger lines and items by 60 to 100 ms.
- Scroll-driven animation uses linear easing; the scroll itself provides the feel.
- Springs with overshoot belong to the playful signature. Elsewhere, motion lands cleanly.

## Craft

- Animate `transform`, `opacity` and `clip-path`. Never width, height, margin or position values.
- Set `will-change` on elements that move during scroll, and only on those.
- Travel far enough to be seen: a headline line rises its full height, an image wipes fully open, a pinned image goes from framed to full screen. Timid movement of a few pixels is worse than none.
- Every entrance plays once.
- Anything shown on hover has a resting state. A photo panel that changes as the pointer moves over a list shows the first item's photo before any hover, and on touch screens. An empty box waiting for a pointer is a bug.
- Use real content inside the motion. A marquee carries the business's own words. A pinned scene tells something true about the business. Never animate filler.

## Limits that do not move

- **The main action is usable at once.** On first paint, before any animation, a visitor can read what the business is and tap the main button. Animate around it, not over it.
- **Reduced motion is respected.** When `prefers-reduced-motion: reduce` is set, nothing is hidden waiting for an animation, pinned scenes become normal sections, video does not autoplay, and smooth scrolling is off. The patterns file is built this way: all motion sits inside one `if (!reduce)` block and hidden states are set by the script.
- **The page works if the script fails.** Content is visible by default.
- **Phones get a lighter version.** Pointer effects are off. Pinned scenes are shorter or become stacked sections. A horizontal gallery becomes a swipeable row.
- **Nothing blocks reading.** No text that types itself out, no content that needs an exact scroll position to be legible, no loading screen that makes the visitor wait.
- **No invented numbers.** Counters that tick up to statistics are only for statistics the business supplied.
- **Smooth scrolling never fights the visitor.** It adds inertia; it does not change direction, snap unexpectedly or take control away.
