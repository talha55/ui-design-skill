# Step 5: Media

A page with no pictures feels unfinished, and a page with broken or invented pictures is worse. Use real photos and video that fit the business, and prove every link works before you use it.

## Sources

- **Photos:** Unsplash (`unsplash.com`). Free to use, no attribution required, though crediting the photographer in a code comment is good manners.
- **Video:** Pexels (`pexels.com/videos`). Unsplash has no video.

Stock media stands in for the business's own photos until they supply them. It is never presented as the business itself.

## Finding the right media

1. Search for the trade plus the photo mood agreed in the direction. Search for the work itself, its materials, its tools and its results, in several different phrasings, and look at more than the first few results.
2. Prefer real working scenes, hands, tools, materials and finished results. Avoid staged shots: models in spotless uniforms giving a thumbs up, handshakes, people pointing at laptops.
3. Choose a set that belongs together: similar light, similar colour temperature, similar distance. Three photos from three different worlds look like a collage.
4. Avoid visible brand names, vehicle signage, and identifiable faces. A stranger's face next to "our team" is a false claim.
5. Use media generously and large. A bold page needs a strong hero image or video and enough supporting photographs to carry its scenes: typically five to eight. Choose high resolution and show them big, full-bleed or close to it. Small thumbnails in boxes waste a good photograph.
6. Check the licence. Some results are paid or members-only images (on Unsplash these are served from a different host than `images.unsplash.com`, or have `premium` in the file name). Do not use them. Do not use 3D renders or illustrations where a photo of real work is meant.
7. Look for a hero video. A short, silent, looping clip of the work, the material or the place does more for a first impression than any still. Search Pexels for one that fits; if none is good enough, use a photograph.

## The verification rule

**Never write a media URL from memory.** A URL that looks right but was never fetched is treated as broken.

For every photo and video:

1. Find it by searching the source, using whatever web search or fetch tool is available.
2. Fetch the exact URL you intend to put in the page, and confirm it loads as an image or a video (an HTTP 200 with an image or video content type).
3. Only then use it.

Photo URLs take this form, with sizing parameters so the browser downloads a sensible size:

`https://images.unsplash.com/photo-<id>?w=1600&q=80&auto=format&fit=crop`

Use a smaller `w` for small images (800 for cards, 1600 to 2000 for a full-width hero).

## When you cannot verify

If you have no tool that can reach the source, or a link does not load:

- Do not guess another URL.
- Put a visible, styled placeholder block in the image's place: a solid surface in a palette neutral with a short label that names the photo needed and says it is to be supplied.
- Add the item to the handover list with a suggested search phrase.

A page with three honest placeholders is finished. A page with three broken images is not.

## Using media well

- Every image has `alt` text that describes what is in the picture. Purely decorative images use `alt=""`.
- Set `width` and `height` so the layout does not jump, and `loading="lazy"` on everything below the first screen. The hero image loads eagerly.
- Crop with `object-fit: cover` to a fixed aspect ratio so rows line up.
- Video: `muted`, `playsinline`, `loop`, a verified `poster` image, no sound, no controls needed for background use. Do not autoplay when the visitor prefers reduced motion; show the poster.
- Text over media needs an overlay dark or light enough to pass contrast at every point, not only where the photo happens to be plain.
- Give image containers a background colour from the palette so the page still reads if media fails to load.
- Treat the photos to match the palette when it helps: a slight tint or a consistent crop style ties stock photos together.
