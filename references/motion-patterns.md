# Motion patterns

Working code for the moves named in `art-direction.md` and `07-motion.md`. Each pattern is small and independent. Take the ones the page needs; do not use all of them on one page.

Every pattern is written for a standalone HTML page and uses [Motion](https://motion.dev). In React, use the same ideas with `motion/react` (`useScroll`, `useTransform`, `whileInView`, `whileHover`).

## Setup

Put this once at the end of the body. Everything else goes inside the `if (!reduce)` block.

```html
<link rel="stylesheet" href="https://unpkg.com/lenis@1/dist/lenis.css">

<script type="module">
import { animate, scroll, inView, stagger, hover, press } from "https://cdn.jsdelivr.net/npm/motion@14/+esm";
import Lenis from "https://cdn.jsdelivr.net/npm/lenis@1/+esm";

const reduce = window.matchMedia("(prefers-reduced-motion: reduce)").matches;
const fine = window.matchMedia("(hover: hover) and (pointer: fine)").matches;
const EASE = [0.16, 1, 0.3, 1]; // fast start, long soft landing

if (!reduce) {
  // Smooth scrolling. Leave this out on a quiet page.
  new Lenis({ autoRaf: true });

  // patterns go here
}
</script>
```

Two rules that keep every pattern safe:

- Hidden starting states are set from the script, never in the CSS. If the script fails or motion is reduced, the content is simply there.
- Pointer effects sit inside `if (fine) { ... }` so they never run on touch screens.

## 1. Headline that rises line by line

The signature opening for editorial and cinematic pages. Each line slides up from behind a mask.

```css
.line { display: block; overflow: hidden; padding-bottom: 0.08em; }
.line > span { display: block; will-change: transform; }
```

```html
<h1 data-lines>The headline, as plain text</h1>
```

```js
function splitLines(el) {
  const words = el.textContent.trim().split(/\s+/);
  el.textContent = "";
  const spans = words.map((w) => {
    const s = document.createElement("span");
    s.textContent = w + " ";
    s.style.display = "inline-block";
    s.style.whiteSpace = "pre";
    el.appendChild(s);
    return s;
  });
  const rows = [];
  let top = null;
  spans.forEach((s) => {
    if (s.offsetTop !== top) { rows.push([]); top = s.offsetTop; }
    rows[rows.length - 1].push(s.textContent);
  });
  el.textContent = "";
  el.setAttribute("aria-label", words.join(" "));
  return rows.map((r) => {
    const line = document.createElement("span");
    line.className = "line";
    line.setAttribute("aria-hidden", "true");
    const inner = document.createElement("span");
    inner.textContent = r.join("").trimEnd();
    line.appendChild(inner);
    el.appendChild(line);
    return inner;
  });
}

document.fonts.ready.then(() => {
  document.querySelectorAll("[data-lines]").forEach((el, index) => {
    const lines = splitLines(el);
    lines.forEach((l) => (l.style.transform = "translateY(110%)"));
    const play = () => animate(lines,
      { transform: ["translateY(110%)", "translateY(0%)"] },
      { duration: 0.9, ease: EASE, delay: stagger(0.08) });
    if (index === 0) play();                       // the first one plays on load
    else inView(el, () => { play(); }, { amount: 0.4 });
  });
});
```

The heading must contain plain text only. Wait for `document.fonts.ready` so the lines are measured in the real typeface.

## 2. Opening sequence

One orchestrated entrance when the page loads: headline first, then the supporting pieces a beat later. Mark the supporting pieces with `data-load`.

```js
animate("[data-load]",
  { opacity: [0, 1], transform: ["translateY(16px)", "translateY(0px)"] },
  { duration: 0.7, ease: EASE, delay: stagger(0.08, { startDelay: 0.45 }) });
```

Do not put `data-load` on the main call button on a page where people arrive in a hurry. It should be there on first paint.

## 3. Image revealed by a wipe

The mask opens while the image settles from a slight zoom.

```css
.reveal-img { overflow: hidden; }
.reveal-img > img { width: 100%; height: 100%; object-fit: cover; will-change: transform, clip-path; }
```

```js
document.querySelectorAll("[data-reveal-img]").forEach((box) => {
  const img = box.firstElementChild;
  img.style.clipPath = "inset(0 0 100% 0)";
  inView(box, () => {
    animate(img,
      { clipPath: ["inset(0 0 100% 0)", "inset(0 0 0% 0)"], transform: ["scale(1.2)", "scale(1)"] },
      { duration: 1.1, ease: EASE });
  }, { amount: 0.3 });
});
```

Change the inset to wipe from another side: `inset(0 100% 0 0)` opens from the left.

## 4. Simple reveal

For ordinary content. Use it sparingly; if everything fades up, nothing stands out.

```js
document.querySelectorAll("[data-reveal]").forEach((el) => {
  el.style.opacity = "0";
  inView(el, () => {
    animate(el, { opacity: [0, 1], transform: ["translateY(24px)", "translateY(0px)"] },
      { duration: 0.7, ease: EASE });
  }, { amount: 0.25 });
});
```

## 5. Pinned scene

The heart of a cinematic page. The section is taller than the screen; its stage sticks in place while scroll position drives the animation inside it.

```css
.scene { height: 300vh; position: relative; }
.scene > .stage { position: sticky; top: 0; height: 100vh; overflow: hidden; display: grid; place-items: center; }
```

```html
<section class="scene" data-scene>
  <div class="stage">
    <img data-scene-plate src="..." alt="...">
    <p data-scene-caption>...</p>
  </div>
</section>
```

```js
document.querySelectorAll("[data-scene]").forEach((scene) => {
  const range = { target: scene, offset: ["start start", "end end"] };
  // The image grows from a framed picture to fill the screen.
  scroll(animate(scene.querySelector("[data-scene-plate]"),
    { transform: ["scale(0.6)", "scale(1)", "scale(1.6)"] }, { ease: "linear" }), range);
  // The caption appears in the middle of the scene and leaves before the end.
  scroll(animate(scene.querySelector("[data-scene-caption]"),
    { opacity: [0, 0, 1, 1, 0] }, { ease: "linear" }), range);
});
```

The height of `.scene` sets how long the scene lasts: 200vh is brisk, 400vh is slow. Keyframe arrays are spread evenly across the scroll range, so `[0, 0, 1, 1, 0]` means hidden for the first quarter, visible in the middle, gone at the end. Several elements can share one scene with different keyframes to build a sequence.

On a phone, shorten the scene (`height: 200vh`) or let it fall back to a normal stacked section.

## 6. Horizontal gallery driven by vertical scroll

```css
.gallery { height: 400vh; position: relative; }
.gallery > .stage { position: sticky; top: 0; height: 100vh; overflow: hidden; display: flex; align-items: center; }
.track { display: flex; gap: 4vw; padding: 0 6vw; will-change: transform; }
.track > * { flex: 0 0 60vw; }
```

```js
document.querySelectorAll("[data-gallery]").forEach((gallery) => {
  const track = gallery.querySelector("[data-track]");
  const distance = () => track.scrollWidth - window.innerWidth;
  scroll((progress) => {
    track.style.transform = `translateX(${-progress * distance()}px)`;
  }, { target: gallery, offset: ["start start", "end end"] });
});
```

Below 768 px, replace this with a normal swipeable row: `overflow-x: auto; scroll-snap-type: x mandatory`, and do not run the script.

## 7. Parallax

An inner layer moves slower than the page. Keep the distance small.

```css
.parallax { position: relative; overflow: hidden; height: 70vh; }
.parallax > img { position: absolute; inset: -15% 0; width: 100%; height: 130%; object-fit: cover; will-change: transform; }
```

```js
document.querySelectorAll("[data-parallax]").forEach((box) => {
  scroll(animate(box.firstElementChild,
    { transform: ["translateY(-12%)", "translateY(12%)"] }, { ease: "linear" }),
    { target: box, offset: ["start end", "end start"] });
});
```

## 8. Marquee band

A line of large text that runs across the page without stopping. The content is duplicated once so the loop has no gap.

```css
.marquee { overflow: hidden; white-space: nowrap; }
.marquee > div { display: inline-flex; gap: 3rem; padding-right: 3rem; will-change: transform; }
```

```html
<div class="marquee" data-marquee><div><span>First</span><span>Second</span><span>Third</span></div></div>
```

```js
document.querySelectorAll("[data-marquee]").forEach((m) => {
  const strip = m.firstElementChild;
  const clone = strip.cloneNode(true);
  clone.setAttribute("aria-hidden", "true");
  m.appendChild(clone);
  animate([strip, clone], { transform: ["translateX(0%)", "translateX(-100%)"] },
    { duration: 24, ease: "linear", repeat: Infinity });
});
```

Use real words from the brief: services, places, the business name. Never filler.

## 9. Scroll progress bar

```css
.progress { position: fixed; left: 0; top: 0; height: 3px; width: 100%; transform-origin: 0 50%; transform: scaleX(0); z-index: 50; }
```

```js
scroll(animate("[data-progress]", { transform: ["scaleX(0)", "scaleX(1)"] }, { ease: "linear" }));
```

## 10. Magnetic button

The button leans towards the pointer and springs back.

```js
if (fine) {
  document.querySelectorAll("[data-magnetic]").forEach((el) => {
    el.addEventListener("pointermove", (e) => {
      const r = el.getBoundingClientRect();
      const x = (e.clientX - r.left - r.width / 2) * 0.3;
      const y = (e.clientY - r.top - r.height / 2) * 0.3;
      animate(el, { transform: `translate(${x}px, ${y}px)` }, { duration: 0.3, ease: "easeOut" });
    });
    el.addEventListener("pointerleave", () =>
      animate(el, { transform: "translate(0px, 0px)" }, { type: "spring", stiffness: 300, damping: 15 }));
  });
}
```

## 11. Cursor follower

A small shape that trails the pointer and grows over links.

```css
.cursor { position: fixed; left: 0; top: 0; width: 18px; height: 18px; border-radius: 50%; pointer-events: none; mix-blend-mode: difference; background: #fff; z-index: 99; transform: translate(-100px, -100px); }
@media (hover: none) { .cursor { display: none; } }
```

```js
if (fine) {
  const cursor = document.querySelector("[data-cursor]");
  window.addEventListener("pointermove", (e) => {
    animate(cursor, { transform: `translate(${e.clientX - 9}px, ${e.clientY - 9}px)` },
      { duration: 0.25, ease: "easeOut" });
  });
  hover("a, button", () => {
    animate(cursor, { scale: 3 }, { duration: 0.25 });
    return () => animate(cursor, { scale: 1 }, { duration: 0.25 });
  });
}
```

Keep the real cursor visible. The follower is an addition, not a replacement.

## 12. Card that tilts towards the pointer

```js
if (fine) {
  document.querySelectorAll("[data-tilt]").forEach((el) => {
    el.addEventListener("pointermove", (e) => {
      const r = el.getBoundingClientRect();
      const rx = ((e.clientY - r.top) / r.height - 0.5) * -10;
      const ry = ((e.clientX - r.left) / r.width - 0.5) * 10;
      animate(el, { transform: `perspective(900px) rotateX(${rx}deg) rotateY(${ry}deg)` },
        { duration: 0.2, ease: "easeOut" });
    });
    el.addEventListener("pointerleave", () =>
      animate(el, { transform: "perspective(900px) rotateX(0deg) rotateY(0deg)" },
        { duration: 0.5, ease: EASE }));
  });
}
```

## 13. Press feedback

```js
press("a, button", (el) => {
  animate(el, { scale: 0.96 }, { duration: 0.12 });
  return () => animate(el, { scale: 1 }, { duration: 0.2 });
});
```

## 14. Atmosphere without script

These need no JavaScript and cost almost nothing.

Grain over the whole page:

```css
body::after {
  content: ""; position: fixed; inset: 0; pointer-events: none; z-index: 100; opacity: 0.06;
  background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='200' height='200'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='2'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)'/%3E%3C/svg%3E");
}
```

A slow, living gradient behind a dark hero:

```css
.aurora { position: absolute; inset: -20%; filter: blur(80px); opacity: 0.6;
  background: radial-gradient(40% 40% at 30% 30%, var(--accent), transparent),
              radial-gradient(35% 35% at 70% 60%, var(--accent-2), transparent);
  animation: drift 18s ease-in-out infinite alternate; }
@keyframes drift { to { transform: translate3d(4%, -3%, 0) rotate(8deg) scale(1.1); } }
@media (prefers-reduced-motion: reduce) { .aurora { animation: none; } }
```

A link underline that draws in on hover:

```css
.link { background: linear-gradient(currentColor, currentColor) 0 100% / 0 2px no-repeat; transition: background-size 0.35s cubic-bezier(0.16, 1, 0.3, 1); }
.link:hover, .link:focus-visible { background-size: 100% 2px; }
```

## Video in the hero

```html
<video autoplay muted loop playsinline poster="verified-poster.jpg" data-hero-video>
  <source src="verified-video.mp4" type="video/mp4">
</video>
```

```js
if (reduce) document.querySelectorAll("[data-hero-video]").forEach((v) => { v.removeAttribute("autoplay"); v.pause(); });
```

The video and the poster are both verified as in `05-media.md`.
