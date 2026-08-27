# Quiet House (`/ha`) — glanceability redesign

**Date:** 2026-08-27
**Status:** design agreed, not yet implemented
**File:** `ha/index.html` (single self-contained page, no Jekyll front matter)

## Problem

The page reads as TL;DR. Measured on the current build:

| Metric | Value |
|---|---|
| Words | 3,299 (~14 min read) |
| Sentences | 209, averaging 15.7 words |
| Prose paragraphs | 111 |
| Headings | 43 |
| Discrete boxes/cards | 53 |
| Content sections | 13 |

Word count is a symptom. The cause is **uniform texture**: all 13 sections share one
shape — eyebrow, headline, lede, grid of boxes, each box tag + h3 + paragraph +
footnote. 53 boxes present as equally important and cost equal reading effort, so the
eye gets no landing point and the page reads as homework.

All body type sits between 13.5px and 21px. The only elements that grab are the four
big figures in Reference Build and the six-mark tile strip — both of which prove the
fix rather than needing one.

The page also breaks its own charter rule: *depth on demand, never depth by default*.

## Goal

Scan the whole page in ~90 seconds; ~1,500 words; every section anchored by something
readable in under two seconds. Detail that survives is detail that earns its place.

## Three governing rules

1. **Two-second rule.** Every section opens with a number, a three-word verdict, or a
   visual. Prose never opens a section.
2. **One-sentence rule.** No card body exceeds one sentence. One lede paragraph per
   section, maximum.
3. **Size contrast.** The glanceable element must be dramatically larger than the body
   text around it. Flat type scale is why the page currently reads flat.

## Section map: 13 → 9

| # | Section | Was | Budget | Anchor device |
|---|---|---|---|---|
| 1 | Hero + glance strip | 96 + 65 | 120 | Six-mark tile strip, moved above the fold |
| 2 | **Five rules** | (was #9, 391) | 90 | Five display-type one-liners |
| 3 | What it buys you | 543 | 190 | Six big figures (see below) |
| 4 | When → then | 455 | 170 | Two-column table, 6 rows |
| 5 | How you control it | 244 + 271 | 250 | Four one-sentence blocks + prompt list |
| 6 | Reference build + rules 6–8 | 434 | 285 | Four big figures, enlarged |
| 7 | How it goes | 184 + 128 | 120 | Four numbered steps, one line each |
| 8 | Engagements | 219 | 180 | Three tiers, bullets retained |
| 9 | Close | 133 | 80 | Contact ledger |

**Total ≈ 1,485 words**, from 3,299.

## Section detail

### 1. Hero + glance strip
Keep the `h1` verbatim — it is the strongest thing on the page. Cut the lede from four
sentences to one. Move the six-mark tile strip up into the first screen so the page's
best glanceable asset is above the fold. Reduce the aside to two lines.

### 2. Five rules (moved up from position 9)
Headline: **"Five rules I don't bend."** Display type ~30px per rule, each with a gloss
of at most twelve words:

1. Nothing requires an app.
2. Every device keeps a physical control.
3. A guest should never know.
4. Everything runs locally.
5. Full control from anywhere.

Payoff line, in petrol, closing the block: *"The first three are the hard ones. Most of
this industry quietly breaks all three."* — currently buried at the bottom of the
charter section and the most persuasive sentence on the page.

Rationale for the move: these five are promises about how the house feels to live in,
which is the right register directly after the hero. Everything below them is then read
through that frame.

### 3. What it buys you — the footnote-to-number move
The six "Running at the reference house" footnotes (~180 words) duplicate the Reference
Build ledger and are the page's largest single redundancy. **Do not simply delete
them** — they are the only place the value claims carry concrete numbers. Distil each to
a figure and promote it to the top of its card in large petrol type:

| Card | Figure |
|---|---|
| Leaving & arriving | **One button** |
| Light that follows you | **12 rooms** |
| Cost, made visible | **33 appliances** |
| Air and comfort | **4 systems** |
| Things that go wrong quietly | **5 alerts** |
| Music & atmosphere | **10 rooms** |

Each card becomes: figure → headline → one sentence. Same information, ~a fifth of the
words, and six new landing points where there were none.

*Open nit:* "4 systems" is the vaguest of the six; "3 rooms of shades" is an alternative
if it reads weak in place.

### 4. When → then
Convert eight long paragraphs to a six-row two-column table. Left column short and in
petrol ("the mailbox opens", "the freezer warms up"); right column one line. Scans like
a spec sheet. Cut the two weakest of the eight. The 20-minutes-before-your-alarm row is
the strongest — keep it first, and keep the "house has no opinion about which one is
correct" beat, compressed.

### 5. How you control it (Ways in + Bring your own AI, merged)
Both sections are about control surfaces, so they merge. Four blocks of one sentence
each (you don't / a switch / any screen / your voice), then the AI prompt list — already
the most glanceable thing in that section — trimmed to five of seven prompts. Jarvis
paragraph reduced to one line.

### 6. Reference build + rules 6–8
The four big figures are already correct; enlarge them further. Cut each ledger row to
~15 words. Append the three technical rules here under a small heading, because this is
where the technically-minded reader already is and each annotates a row already present:

- Your whole network travels with you → the network/compatibility rows
- Privacy is a design constraint, not a setting → the self-monitoring row
- All the data, none of the noise → the 3,043 tracked things

### 7. How it goes (How I work + Process, merged)
Four numbered steps, one line each, laid out horizontally. The four "creed" cards
(no hacks / you approve first / one source of truth / tuned to your life) reduce to a
single line of chips beneath the steps.

### 8. Engagements
Trim lightly. Pricing tiers need their specifics, and bullet lists are already
glanceable. Cut the intro lede to one sentence.

### 9. Close
Two sentences, the CTAs, and the existing serving/good-fit/not-a-fit/capacity ledger,
which already scans well.

### Rhythm breaks
Two full-width pull quotes in large display type between sections, to reset the eye. One
is the deleted Invisibility section's line: *"The whole point is that you never see the
machinery."*

## Deleted outright

- The Invisibility section (112 words) → survives as a pull quote.
- The six card footnotes (~180 words) → survive as six figures.
- Two of the eight when→then pairs.
- Two of the seven AI prompts.
- Per-section ledes wherever the section's anchor device already makes the point.

## Knock-on changes

- **Nav anchors.** Merging Ways in + Ask removes `#ask`; nav drops to five links plus
  the CTA (What it buys you · How you control it · The rules · Reference build ·
  Engagements). This frees ~140px in the bar, so the 1180px collapse breakpoint can come
  down — re-measure and lower it.
- **New CSS components:** figure-led card variant, when→then table, pull-quote band,
  rules list. Reuse existing tokens; introduce no new colours.

## Must not regress

Recent fixes that the rewrite must preserve:

- All text ≥ 4.5:1 contrast (current worst: 5.87:1).
- No horizontal overflow at any width — keep `minmax(0,1fr)` on the tile grids.
- Nav: nothing wraps, CTA is a fixed 40px pill inside the 68px bar.
- Smooth anchor scrolling with `scroll-padding-top`, disabled under reduced motion.

## Verification

1. Re-run the word-count script: total ≤ 1,600.
2. No card body longer than one sentence.
3. Every section's first child is a non-prose element.
4. Re-run the contrast audit: every sampled style ≥ 4.5:1.
5. Screenshot at 390 / 1024 / 1280 / 1440; zero horizontal overflow at each.
6. Every nav anchor resolves to an existing id and lands clear of the sticky bar.

## Out of scope

- Placeholder contact details (`hello@quiethouse.co`, `+1 617 555 0142`) — still live on
  the published page and need real values before the link is shared.
- Linking `/ha` from the site nav.
- Any change to `/fenwick` or the rest of the site.
