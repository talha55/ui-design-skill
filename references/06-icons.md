# Step 6: Icons

Icons help people scan. They do not decorate, and they do not replace words.

## Which icons

- **Static icons:** Lucide (`lucide.dev`).
- **Animated icons:** the animated Lucide set (`lucide-animated.com`), for icons that respond to hover or to a change of state.

One family per page. Do not mix in another icon set, hand-drawn SVGs in a different style, or emoji.

## Using Lucide

Plain HTML:

```html
<script src="https://unpkg.com/lucide@latest"></script>
<i data-lucide="phone" aria-hidden="true"></i>
<script>lucide.createIcons();</script>
```

React or Next.js:

```jsx
import { Phone } from "lucide-react";
<Phone size={20} strokeWidth={1.75} aria-hidden="true" />
```

Use icon names that exist. If you are not certain a name exists, check the Lucide site or choose a common one (`phone`, `mail`, `map-pin`, `clock`, `calendar`, `arrow-right`, `check`, `menu`, `x`).

## Using animated icons

The animated set ships as React components that are copied into the project. In a React or Next.js project, add an icon with the command documented on its site (`npx shadcn@latest add @lucide-animated/<icon-name>`), then import it from where it was placed.

In plain HTML there is no animated set to load. Use the static Lucide icon and give it a small Motion hover instead (see step 7): a few pixels of movement, a slight rotation or a gentle scale. That is the fallback, and it is enough.

Animate an icon only when it reacts to something the visitor did. Icons that move on their own distract.

## Rules

- **Size:** one size per context. 16 to 20 px beside text, 24 px in buttons and lists, up to 32 px as a feature marker. Do not scale icons up to fill space.
- **Stroke:** one stroke width for the whole page. 1.5 to 2 suits most pages; match the weight of the text beside it.
- **Colour:** icons take the text colour or the dominant colour. Reserve the accent for the primary action.
- **With labels:** an icon accompanies a label. The primary action always has words. Icon-only buttons are for universal controls such as a menu or close button, and they get an `aria-label`.
- **Decorative icons** get `aria-hidden="true"`.
- **Restraint:** not every heading or list item needs an icon. If removing an icon loses nothing, remove it. A section of six services with six icons in coloured circles is the most common generated pattern; prefer a plain list, numbers, or photos.
- **Alignment:** icons sit on the centre line of the text beside them, with a consistent gap of 8 or 12 px.
