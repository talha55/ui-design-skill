---
name: ui-design-skill
description: Plan, design and build a marketing website or landing page for a business, product or person, or redesign one. Use when asked to build, create or redesign a website, homepage or landing page. Agrees a design direction first, uses real verified photos and video, Lucide icons, Motion animation, and never invents facts about the business. Not for dashboards, internal tools or mobile apps.
---

# UI Design Skill

Build a page a working designer would sign their name to, and that says nothing untrue about the business it is for.

Most generated sites fail in the same three ways: they look like every other generated site, their images are broken or invented, and they are full of made-up reviews and numbers. This skill exists to prevent those three failures. Work through the eight steps in order. Do not skip a step because the request looks small.

## Order of precedence

When two rules pull against each other, the higher one wins:

1. What the person asked for.
2. The business's existing brand: its logo, colours, typeface and tone, when supplied.
3. Honesty: nothing invented about the business.
4. Accessibility: contrast, focus states, reduced motion.
5. The direction agreed at the checkpoint.
6. Visual flourish.

## The eight steps

Read the named reference file before each step. Each one is short. Do not work from memory of an earlier step's file.

1. **Plan.** Decide who the page is for, the one action it should drive, the structure, the style, the palette and the type. Read `references/01-plan.md`.
2. **Direction checkpoint.** Show a short direction summary and wait for a yes. Read `references/02-direction.md`.
3. **Build.** Build the agreed direction, mobile first, section by section. Read `references/03-build.md`.
4. **Polish.** A separate pass over alignment, rhythm, states and contrast. Read `references/04-polish.md`.
5. **Media.** Real photos and video that fit the business, every link checked. Read `references/05-media.md`.
6. **Icons.** Lucide, one family, used with restraint. Read `references/06-icons.md`.
7. **Motion.** Purposeful animation with the Motion library. Read `references/07-motion.md`.
8. **Final check.** Remove what makes a page look machine-made, and remove anything invented. Read `references/08-final-check.md`.

Steps 5 to 7 are written as separate steps so that none is forgotten. In practice you choose media, icons and motion while building. What matters is that each file's rules are applied before the final check.

## The checkpoint rule

After step 2, stop and wait for an answer. Do not build "a quick first version" while waiting.

Skip the wait only when:

- the request says to just build it, or says not to ask questions, or
- the person has already given the direction (style, colours and structure), or
- you are running where nobody can answer.

When you skip the wait, still write the direction summary, state it in one short paragraph at the top of your reply, and build to it.

## Stack

Follow the project you are in. Use its framework, its styling approach and its components.

With no existing project, build one self-contained HTML file:

- Tailwind from its CDN script for styling.
- Lucide from `https://unpkg.com/lucide@latest`, then `lucide.createIcons()`.
- Motion as an ES module from `https://cdn.jsdelivr.net/npm/motion@latest/+esm`.
- Fonts from Google Fonts with `display=swap`.

In a React or Next.js project, use the `lucide-react` and `motion` packages (`import { motion } from "motion/react"`).

## Never

- Never write a photo or video URL from memory. Every media URL is fetched and seen to load, or it is not used.
- Never invent a fact about the business: no reviews, ratings, statistics, awards, client logos, team members, prices, guarantees, years in business or licence numbers that were not supplied.
- Never replace a supplied logo, colour or typeface with one you prefer.
- Never mix icon families, and never use emoji as icons.
- Never ship without the final check.

## Finish with a handover list

End your reply with a short list titled "Still needed from you": every placeholder on the page and what should replace it (logo, real photos of the team and vans, reviews, licence details, pricing, and anything else the page would be stronger with). This list is part of the work, not an apology. A page with honest gaps is finished; a page with invented content is not.
