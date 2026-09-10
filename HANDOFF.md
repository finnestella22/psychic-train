# Handoff: Section 222 (NY Rangers lifestyle brand site)

**Live site:** https://finnestella22.github.io/psychic-train/
**Repo:** https://github.com/finnestella22/psychic-train (single `main` branch, GitHub Pages serves it directly — no build step)
**Stack:** One static `index.html` (inline `<style>` + inline `<script>` at the bottom), plus `news.json` and a handful of PNG assets in the repo root. No framework, no bundler, no package.json. Edit the file, commit, push — Pages redeploys in under a minute.

## What this is

"Section 222" — an independent NY Rangers-inspired hockey lifestyle/streetwear brand concept site. Dark theme (black bg, Rangers blue accent), collegiate/varsity typography (Oswald for headlines/nav/numerals, Graduate for the "222" numeral mark, Readex Pro for body copy). Sections in order: hero (cursor-spotlight photo reveal + "BLEED/BLUE/NYC" headline), a scrolling fan-chant ticker, "The Drop" product grid, "Rangers News" (reads from `news.json`), contact/order, footer.

Brand voice: restrained and dry in core copy (nav, product names, contact copy) — NOT the loud meme-chant voice, which is deliberately contained to the ticker only. Reference line for tone: *"An independent NY hockey label. Small-batch runs on heavyweight blanks — once they're gone, they're gone."*

No real backend or checkout anywhere. "Order Now" / product tiles / contact CTA are all `mailto:` links to the owner's email. This is intentional for now (soft-launch/concept stage), not an oversight.

## Mobile nav — fixed

`.nav-center` is still `display: none` below 768px (unchanged), but there's now a real hamburger (`.nav-toggle` / `#navToggle`) next to "Order Now" that opens a dropdown (`.mobile-menu` / `#mobileMenu`) with the same 5 links, toggled by a small script near the bottom of the file. Note: nav content is tight at narrow widths — there's a `@media (max-width: 480px)` block right after `.nav-right:hover` that shrinks the logo/button/toggle to keep everything on one row and stop the hamburger from overflowing off-screen (it did originally; fixed by that block). If nav content changes, re-check at 375px width that nothing clips off the right edge.

## Minor polish (do if convenient, not urgent)

- No favicon set at all (`<link rel="icon">` is absent). Should get one.
- CTA copy says "Order Now" but there's no real checkout — just opens a mailto draft. Reasonable for now, but if this goes wider, consider "Join the waitlist" / "Request early access" instead so it doesn't overpromise.
- The 3 "founding drop" products (222 Varsity Tee, Broadway Blueshirt Hoodie, Home Ice Flag) use placeholder product photography — real Comfort Colors blanks (recolored Printful catalog photos), explicitly tagged "Founding Drop — Concept" in the UI. Swap for real photos once the owner has actual prints made.

## News section — how it works, what's pending

`news.json` at the repo root is a simple array (`date`, `title`, `blurb`, `link`, optional `image`), rendered client-side by the `fetch('news.json')` block at the bottom of `index.html`. Cards show the image (16:9, bleeds to card edges) when present.

Currently has **one real entry**, manually researched and added (not automated yet): a Sept 4, 2026 story about Adam Fox trade rumors being dismissed, sourced from The Hockey Writers with a real image/link pulled from that article's `og:image`.

**The plan** (agreed with the owner, not yet live): a recurring job every 3 days that searches for significant Rangers news (NHL.com/beat reporters prioritized over Reddit — Reddit only as a "check if this is big" signal, never cited as the source), writes a condensed headline + blurb in brand voice, pulls the real source article's image, and pushes to `main` fully autonomously (no human check-in, per owner's explicit choice). If nothing significant happened in a 3-day window, the job should skip rather than invent filler — a quiet news tab beats fake news.

**Blocker:** creating this as a claude.ai scheduled routine failed with `Connect your GitHub account before saving a routine that uses a GitHub repository` — the owner's claude.ai account isn't connected to GitHub yet (separate from any local git/SSH setup on their machine). They need to visit https://claude.ai/code/onboarding?magic=github-app-setup and connect it before the routine can be created. Once connected, the full routine spec (sourcing rules, brand-voice examples, image-linking approach, idempotency/dedup logic, 12-entry rolling cap) is ready to paste into a `RemoteTrigger` create call — ask the owner for the exact prompt if it wasn't preserved, or reconstruct it from this doc's "the plan" paragraph above.

## Trademark/legal notes

- Fonts: the site does **not** use the NHL's real broadcast typeface (an earlier version pulled it from a font-piracy site) — replaced with licensed Google Fonts (Oswald/Graduate/Readex Pro). That part's a hard requirement, not a judgment call.
- Hero photo (`crew.png`): this **does** show the real "RANGERS" jersey wordmark and NHL shield — it was cropped at one point specifically to hide those, but the owner explicitly decided they don't care about that exposure and asked for the full, uncropped photo restored (all 4 subjects fully visible, gesture and jerseys included). That's a deliberate, informed call by the owner, not an oversight — don't "fix" it back to a crop without asking first.

## Brand facts worth knowing

- Brand name "Section 222" comes from a real detail: it's the ticker line "FOR THE FAITHFUL IN SECTION 222" that already existed in the site's fan-chant copy before the rebrand, and ties to the owner's own email handle.
- Color: Rangers blue (`#0038a8`-ish) as the dominant accent on black, not a neutral/desaturated palette — this was an explicit choice over a more muted KITH-style palette.
- Inspirations discussed with the owner: Soda Sports (small-batch vintage bootleg tees), Old Jewish Men of NY (hyper-local deadpan humor as a lifestyle brand), KITH (restrained minimal typography), New York or Nowhere (varsity/collegiate NYC pride, organic-only marketing, no paid ads).
