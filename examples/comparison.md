# With and without the skill (version 1.0)

This test was run on version 1.0, the first, restrained version of the skill. Version 1.1 aims much higher by default; see the [showcase](showcase) for what it produces. The results below still describe version 1.0 accurately, and the rules they measured (verified media, one icon family, nothing invented) are unchanged in 1.1.

The same brief, built six times: three times with no skill and three times with UI Design Skill. This page says exactly how the test was run and what it showed, including where the skill made no difference.

## Method

- **Brief:** [brief.md](brief.md), an invented plumbing and gas business with no logo, colours, photos or reviews supplied.
- **Model:** Claude Sonnet, on 5 October 2026. Each build ran in a fresh session with no memory of the others.
- **Without the skill:** the session was told to use no skills and build the page as a single file.
- **With the skill:** the session was told to follow this skill and no other. The brief had "Just build it, I trust your judgement" added, so the direction checkpoint was skipped and the direction was written down instead ([direction.md](direction.md)).
- **Scoring:** the six pages were given neutral names and scored by a separate session that did not know which pages used the skill. It saw desktop and mobile screenshots and the code, and marked each rubric item yes or no.
- **Which pair is shown:** the median-scoring page from each group, not the best against the worst. Ties were broken by the lower run number.

## Rubric

1. One clear primary action on the first screen, on desktop and mobile.
2. Sections vary in shape; the page is not a centred hero over a grid of identical icon cards.
3. The palette suits a trade business and is not a default purple gradient.
4. A deliberate type pairing on a consistent scale.
5. Consistent spacing between sections and inside components.
6. Real photos or video of relevant subjects, and every one loads.
7. Icons from one family, no emoji as icons.
8. Restrained motion, with reduced motion respected.
9. Nothing stated about the business beyond the brief.
10. Works at 390 px wide.

## Results

| Run | Total out of 10 |
|---|---|
| Without, run 1 | 5 |
| Without, run 2 | 6 |
| Without, run 3 | 6 |
| With, run 1 | 10 |
| With, run 2 | 9 |
| With, run 3 | 10 |

Runs passing each item, out of three:

| Item | Without | With |
|---|---|---|
| 1. Primary action | 3 | 3 |
| 2. Varied layout | 0 | 3 |
| 3. Palette | 3 | 3 |
| 4. Type pairing | 2 | 3 |
| 5. Spacing | 3 | 3 |
| 6. Real photos that load | 0 | 3 |
| 7. One icon family | 0 | 3 |
| 8. Motion, reduced motion respected | 3 | 3 |
| 9. Nothing beyond the brief | 0 | 2 |
| 10. Works at 390 px | 3 | 3 |

The pair shown in this folder is "With, run 1" (10) and "Without, run 2" (6).

## What differed

- **Photos.** No page built without the skill used a single photo. Every page built with it used two or three Unsplash photos, each fetched and confirmed to load before use, with a footer line saying they are stock and do not show the business.
- **Layout.** Without the skill, all three pages put the services in a grid of icon cards. With it, services became numbered lists beside a photo, split sections and full-width bands.
- **Icons.** Without the skill, icons were hand-written inline drawings in mixed styles. With it, every icon came from Lucide.
- **Type.** With the skill, every page loaded a chosen heading and text typeface. Without it, the pages used system fonts, and one used a single font stack with no pairing.
- **Invented details.** This was the largest surprise. The brief says plainly that no reviews or licence numbers were supplied, and no page invented those. But all three pages built without the skill added smaller facts that were never given: "Sunday: Closed", "qualified gas fitter", "most jobs finished in one visit", "fully equipped vans", a three-step process with "pay after you see the result". With the skill, the same gaps became dashed placeholders ("Opening and closing times to be supplied") and a list of what the owner still has to provide. One page built with the skill still added a line ("Open for booked work and quotes") and lost the point.

## What did not differ

- Every page, with or without the skill, had a clear call button on the first screen, a sensible palette, consistent spacing, working mobile layout and reduced-motion handling. The model does these well unaided.
- Every page, with or without the skill, chose a teal palette. A business named Tidewell pulls that way. The skill changed the accent and the typefaces between runs, not the dominant colour.
- The pages built without the skill are not bad pages. Their typography and hero sections are tidy, and one has a good service-area diagram. The skill's gains are specific: real media, a designed layout, one icon set, and honesty about gaps.

## Limits

- One brief, one model, three runs each. A different brief or model may show a larger or smaller gap.
- Results vary from run to run. The table above shows the spread.
- The skill went through one revision during testing. An earlier version contained an example sentence that all three test builds copied, so every page came out in the same style. The examples were rewritten and the builds were run again; the results above are from the revised skill.
- Photo links can stop working over time. The skill checks them at build time only.
- The scorer judged screenshots taken with reduced motion switched on, so entrance animations were judged from the code, not seen.
- With the skill, a build took several times longer, because finding and checking photos takes many steps.

## Other behaviour that was tested

- **The checkpoint.** With a person available to answer and no "just build it", the skill produced a direction summary, asked "Build this, or change something?" and built nothing.
- **A supplied brand.** Given fixed brand colours and a typeface, the build used exactly those and added no accent of its own. Where the supplied orange failed contrast against the supplied navy, it used a darker navy for the text on the button and said so.
