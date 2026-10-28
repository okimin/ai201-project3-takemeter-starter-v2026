# TakeMeter
## FOR LATER
device: mps  (Apple Silicon GPU (MPS))
torch:  2.14.1

> ### 👋 Start here
>
> **New to this repo? Read [RUNNING.md](RUNNING.md) first** — setup, the
> notebook, the baseline, and what to do when something breaks.
>
> Once `python test.py` passes:
>
> ```bash
> head -5 data/practice_labels.csv     # the shape your labels.csv needs
> ```
>
> Then open `takemeter.ipynb` **in this folder** — in VS Code, or with
> `jupyter notebook` if you prefer. Pick the kernel: the `.venv` inside this
> project. Run section 1, which reports the hardware you'll be training on.
> Everything else waits until you have data.
>
> Nothing to upload, nothing to connect, no accounts and no keys. The notebook
> runs on your machine and writes next to your code.
>
> **The rest of this file is your submission.** Fill it in as you go.

---

<!-- ─────────────────────────────────────────────────────────────────────────
     HOW TO USE THIS FILE

     Unit 5 asks for the first five sections. Unit 6 adds the five below them.

     Everything is pasted as TEXT. No screenshots, no images.

     ⚠️ The confusion matrix especially. The notebook prints one as a markdown
     table, ready to copy. A screenshot of a matrix earns nothing. Paste the
     table.
     ───────────────────────────────────────────────────────────────────────── -->

<!-- ═══════════════════════ UNIT 5 — THE BUILD ═══════════════════════ -->

## What This Does

<!-- Your community, and what your classifier sorts posts into. Three or four
     sentences. -->
The community was Reddit with a story on a woman's boyfriend treatment against her insecurity. The classifer were split into support, anedote and pushback. Some were harder to classify compared to others.


---

## Label Taxonomy

<!-- Each label: a one-sentence definition and two real examples from your
     reading. Then your decision rule for the hardest boundary.

     The decision rule is worth a point on its own and it's the thing most
     people leave out. Every taxonomy has a hardest boundary. Name yours. -->

### `support`

**Definition:** A comment whose main point is backing OP or someone else in
the thread (praise, comfort, congratulations, or telling them they deserve
better), with any mention of the commenter's own life kept to a passing clause.

**Example 1:**
> Literal life goals. What a man! Keep him. Gosh it's nice to not say "throw the whole man away." He's a gem.

**Example 2:**
> Girrrrl you don’t deserve that. Why isn’t he an ex??? You don’t proudly publicly humiliate some one you love.

### `anecdote`

**Definition:** A comment whose main point is a story or experience from the
commenter's own life (their partner, their skin, a past relationship), even if
it opens or closes with a line of encouragement for OP.

**Example 1:**
> This right here, OP. I met a guy once who did the same thing for me. We’ll be married 9 years next month. He still does it every single day.

**Example 2:**
> Meanwhile my boyfriend told me I should “fix my face” when I had a flare up of rosacea

### `pushback`

**Definition:** A comment that disagrees with OP or another commenter, or
questions the post itself, whatever its tone.

**Example 1:**
> I mean, isn’t this is kinda bare minimum, telling your partner you’re attracted to them and think they’re beautiful as they are? Yes it’s very sweet, but it doesn’t mean they’re THE ONE.I wish op all the luck in love and hope their partner is the one for them! Just musing.

**Example 2:**
> AI almost always uses – or —, and few people do. Now there’s an over-association

### The hardest boundary

**Which two labels:** `support` and `anecdote`

**The decision rule I used every time:**
If the commenter's own story takes up more of the comment than the words aimed
at OP, it's `anecdote`; otherwise it's `support`. A one-clause mention ("I have
one too!", "reminds me of my bf") never makes a comment `anecdote`. Skincare
advice follows the same rule: if it rests on what worked for the commenter or
someone they know, it's `anecdote`. Harsh words about OP's boyfriend are
`support`, not `pushback`, because they side with OP.



---

## The Dataset

<!-- Where you collected from, how you labelled, your counts, and three hard
     cases. -->

**Where the posts came from:**
https://www.reddit.com/r/GirlDinnerDiaries/comments/1wr9s18/my_boyfriend_tells_me_every_day_and_i_never/
**How I labelled them:** <!-- Cold first? Pre-labelled with AI and corrected?
Say so plainly — the disclosure is required, not penalised. -->
They were prelabelled due to time constaints, but were checked, especially on the pushback side.

**Counts per label:**

| Label | Count | Share |
|---|---|---|
| support | 97 | 65% |
| anecdote | 35 | 23% |
| pushback | 18 | 12% |
| **Total** | 150 | 100% |

**Three hard cases**

<!-- Any post that made you pause: what it was, which two labels it could have
     been, and what you chose. These are worth more than the easy 190. -->

**1.**
> *The post:*
>"Hey OP, boy lurker here but your post struck a chord. For 12 years I've been on a daily mission to tell my girlfriend how beautiful she is and to tackle her insecurities. Trust your boyfriend, he's right and you're beautiful"
> *Could have been:* Support
> 
> *I chose, because:* His story took up most of the content of the comment

**2.**
> *The post:*
> That is super sweet, but from a dermatology standpoint you don't have to suffer… Please see a dermatologist… I have had ocular rosacea my whole life. It has improved so much with treatment.
> *Could have been:* support
>
> *I chose, because:* Gave her own experience with Rosnea

**3.**
> *The post:*
> Some of us are in the TRENCHES and the bar is in hell
> *Could have been:*
> support
> *I chose, because:* was arguing about the quality people have been going through not having  similar treatment like the orginal person


---

## The Training Run

<!-- Your starting model, your settings, and anything you changed and why. -->

**Base model:**

**Settings:** <!-- epochs, learning rate, batch size, seed -->

**Anything I changed from the defaults, and why:**

**Split sizes:** <!-- train / val / test, and per-label counts in the test
split. If a label had fewer than about 8 in test, say so — it explains a lot
of next unit's variance. -->



---

## How I Used AI

<!-- Two specific moments — what you asked, what came back, what you changed.

     ⚠️ Plus disclosure of any pre-labelling. If you had a model pre-label a
     batch and then read and corrected every one, say that. It's an allowed
     workflow and disclosing it costs you nothing. Not disclosing it is the
     problem. -->

**Moment 1**

- *What I asked for:* Come up with 3 labels to help suggest 
- *What came back:*Good categorization on the labels as well as what posts go under it.
- *What I changed:*

**Moment 2**

- *What I asked for:*
- *What came back:*
- *What I changed:*

**Pre-labelling disclosure:**

<!-- ═══════════════════════ UNIT 6 — THE TEST ═══════════════════════

     Don't fill these in during unit 5.
     ═══════════════════════════════════════════════════════════════════ -->

---

## Baseline vs. Trained

<!-- Both models on the same posts. `python baseline.py --trained results.json`
     prints this table for you. -->

| Measure | Baseline | Trained | Difference |
|---|---|---|---|
| Overall accuracy | 0.217 | 0.652 | +0.435 |
| Macro F1 | 0.217 | 0.263 | +0.046 |
| F1 — `anecdote` | 0.400 | 0.000 | -0.400 |
| F1 — `pushback` | 0.250 | 0.000 | -0.250 |
| F1 — `support` | 0.000 | 0.789 | +0.789 |

**What I predicted before I looked:**
<!-- Milestone 1 asks you to write this BEFORE seeing the trained numbers. A
     prediction made afterwards isn't one. -->
     I predict that the trained will have more accuracy than the baseline.

**What the gap actually means:**
<!-- If the baseline matched your trained model, your fine-tuning added
     nothing — and that is a real finding, not a failure. Say it plainly. -->

Interesting that the support has accuracy of 0.



---

## Run Log — Before

<!-- Five criteria across three seeds. The notebook's section 6 prints the
     spread table; the Target and Verdict columns are yours. -->

| Measure | Seed 42 | Seed 7 | Seed 2024 | Spread |
|---|---|---|---|---|
| Overall accuracy | 0.652 | 0.652 | 0.739 | 0.087 |
| Macro F1 | 0.263 | 0.263 | 0.468 | 0.205 |
| F1 — `anecdote` | 0.000 | 0.000 | 0.571 | 0.571 |
| F1 — `pushback` | 0.000 | 0.000 | 0.000 | 0.000 |
| F1 — `support` | 0.789 | 0.789 | 0.833 | 0.044 |

Accuracy moved 0.087 across seeds. Enough that a criterion landing within that band can't really be called either way.

| Criterion | Target | Seed 42 | Seed 7 | Seed 2024 | Verdict |
|---|---|---|---|---|---|
| 1. Macro F1 | ≥ 0.45 | 0.263 | 0.263 | 0.468 | MISSED |
| 2. `anecdote` F1 | ≥ 0.40 | 0.000 | 0.000 | 0.571 | MISSED |
| 3. `pushback` recall | ≥ 0.50 | 0.00 (0/3) | 0.00 (0/3) | 0.00 (0/3) | MISSED |
| 4. Agreement with staff labels | ≥ 75% | 80% | 80% | 80% | MET |
| 5. Confidence gap (top third − bottom third accuracy) | ≥ 0.40 | 0.714 | 0.857 | 0.714 | MET |

Criterion 4 is a single check of my labels against the staff set, so it doesn't
change with the seed. The same 80% applies to all three columns.

### Confusion matrix

<!-- ⚠️ TYPED AS A MARKDOWN TABLE. The notebook prints one ready to paste.
     An image of a matrix earns nothing. -->

| true \ predicted | anecdote | pushback | support |
|---|---|---|---|
| **anecdote** | 0 | 0 | 5 |
| **pushback** | 0 | 0 | 3 |
| **support** | 0 | 0 | 15 |

Biggest confusion: 5 real `anecdote` posts called `support`.
The other direction: 0 real `support` posts called `anecdote`.

That's lopsided — the model leans toward `support` on this pair.
A direction like that usually points at your labelling rather than the
model. Your agreement report is the thing that can tell you which.


**My biggest off-diagonal number, and what it means:**
<!-- Not "the model made mistakes" — WHICH boundary it didn't learn, and which
     direction. "7 real analysis posts were called hot_take and only 3 went the
     other way" is a direction, not just an error rate. -->



---

## Verdicts and Diagnoses

<!-- MET or MISSED against LAST UNIT's target. The target has to hold across
     all three seeds, not turn up sometimes. -->

| # | Criterion | Target | Verdict | How I decided |
|---|---|---|---|---|
| 1 | Macro F1 | ≥ 0.45 on every seed | MISSED | 0.263 / 0.263 / 0.468. Only seed 2024 cleared it, and only by 0.018. It has to hold on all three. |
| 2 | `anecdote` F1 | ≥ 0.40 on every seed | MISSED | 0.000 / 0.000 / 0.571. Seeds 42 and 7 never predicted `anecdote` at all. |
| 3 | `pushback` recall | ≥ 0.50 on every seed | MISSED | 0 of 3 on every seed. The model never predicted `pushback` once. |
| 4 | Agreement with staff | ≥ 75% | MET | 24 / 30 = 80% in `agreement_results.json`. This is one check of my labels, not a per-seed number. |
| 5 | Confidence gap | ≥ 0.40 on every seed | MET | 1.000 − 0.286 = 0.714, 1.000 − 0.143 = 0.857, 1.000 − 0.286 = 0.714. It holds on all three. One caveat: on seeds 42 and 7 the model predicts `support` for everything. The "confident third" is just the most support-sounding posts, and those are support posts. So the model passed, but this criterion can't tell a useful confidence signal apart from a collapsed model. |

> Note on criterion 3: my criteria were written when I expected 16 test posts
> with 2 `pushback`. The final dataset is 150 posts, so the test split is 23
> with 3 `pushback`, and 0.50 recall now means 2 of 3. The criterion is still
> measurable, so I haven't revised it, and at 0 of 3 the verdict is the same
> either way.

**Diagnoses**

<!-- For each miss: the cause, and how you know. The four common causes are:
     too few examples for a label, a boundary you applied inconsistently, a
     genuinely hard label pair, and a task the model can't reach from this
     much data.

     ⚠️ Use your agreement report as evidence. It is the only instrument you
     have that can tell a LABELLING problem from a MODEL problem, and this
     section is graded on whether you used it that way. -->

**Miss 1: Macro F1 (cause: too few examples for the minority labels)**

Macro F1 is the average of the three per-label F1s, and `support` was never the
problem: it scored 0.789 / 0.789 / 0.833. This miss is entirely caused by
misses 2 and 3. On seeds 42 and 7, `anecdote` and `pushback` both score 0, so
macro F1 is 0.789 ÷ 3 = 0.263. That is exactly the "always say support" floor I
predicted in criteria.md when I set this target. Seeds 42 and 7 produced
identical results: all 23 test posts were predicted `support` (confusion
matrix: column `support` = 5 / 3 / 15, every other column 0). The model never
learned to leave the majority class. Seed 2024 only cleared 0.45 because it
picked up 2 of the 5 anecdotes.

**Miss 2: `anecdote` F1 (cause: too few examples, with my labelling as a secondary suspect)**

`anecdote` F1 is 0.000 / 0.000 / 0.571. I think this is mainly a data problem,
not a labelling problem, for three reasons:

1. **The model isn't confusing the boundary, it's ignoring the label.** If I
   had labelled support vs. anecdote inconsistently, I'd expect wrong
   predictions in *both* directions: some anecdotes called support and some
   support posts called anecdote. Instead, two seeds predict `anecdote` zero
   times. When seed 2024 does use it, it is right every time (precision 1.0, 2
   of 2), and no `support` post was ever called `anecdote`.
2. **The label isn't unreachable from text.** The zero-shot baseline, which
   never saw my training data, got `anecdote` recall of 0.60. So the signal is
   in the posts. My fine-tuned model just never got pushed off the majority
   class: about 24 `anecdote` training examples against about 68 `support`,
   trained for 3 epochs × 7 batches = 21 updates in total.
3. **My agreement report says my labelling is mostly consistent.** At 80%
   against staff, I passed my own 75% bar.

But the agreement report is also why I can't fully clear my labelling. All six
of my disagreements went to staff, all were pile (a), and five of them were the
same mistake: I let a post's *tone* override what the rule says about its
*structure*. My support/anecdote rule is a structural one too ("whose part is
longer?"), and many anecdotes open warmly before the story. A test example is
"He sounds like a keeper! I went on a makeup course as part of my cancer
treatment…". If I made the tone-over-structure mistake on 5 of 30 staff posts
with the rules in front of me, some warm-opening anecdotes in my AI-pre-labelled
training data have probably ended up as `support`. That would push the model in
exactly the direction the matrix shows (5 of 5 anecdotes → `support` on two
seeds). So the main cause is too few examples, and the second suspect is
inconsistent labelling on the support/anecdote boundary. A relabelling pass on
that boundary would test the second.

**Miss 3: `pushback` recall (cause: too few examples for a label that is really three different things)**

The model got 0 of 3 on every seed and never predicted `pushback` once. There
are only about 12–13 `pushback` examples in training (18 total, 70% split).
Those 18 aren't one pattern. They split into three groups:

- **Accusing OP of using AI:** "Thanks chatgpt", "Beige flag cause it was written with ai"
- **Disagreeing with OP's framing:** "isn't this kinda bare minimum…", "Eh, I'd be wary of the 'I haven't missed a day…' thing"
- **Defending OP against the AI accusers:** "So tired of all the AI accusations…", "Same! It's like if someone writes well, it must be AI…"

The third group is `pushback` under my rule ("disagrees with OP *or another
commenter*, whatever its tone"). But its words side with OP, so on tone alone
it reads as `support`. That is the same tone-vs-structure gap my agreement
report caught me falling into. Here, though, the agreement report points to
the model rather than my labels. I applied "whatever its tone" consistently:
every AI-defence comment is `pushback`. The issue is that a model with about 12
mixed examples learns tone, not who a comment is arguing with. Two of the three
test `pushback` posts are the hard kind: "Same! It's like if someone writes
well…" (an AI defence that sounds supportive) and "Eh, I'd be wary…" (which
starts gently). The zero-shot baseline caught 2 of the 3 (recall 0.67), so the
label can be reached from the text. My fine-tuned model just had too few
examples, split across three sub-patterns, to learn it. So this is too few
examples combined with a genuinely hard pair (`pushback` vs. `support`), and
the difficulty comes from how I defined the label, not from applying it
inconsistently.



---

## Agreement Report

<!-- Your rate against the staff set, and every disagreement adjudicated.

     Remember you labelled these 30 under the STAFF taxonomy in
     data/staff_taxonomy.md, not your own — so every argument below is made
     from those definitions and those decision rules. -->

**Agreement rate:** 24 / 30 = 80%

<!-- Nobody grades this number. A 60% who argues every disagreement from the
     stated rules beats a 95% who wrote "staff was right" nine times. Several
     of the 30 were chosen because they're genuinely ambiguous — you should be
     winning some of these. -->

**Disagreements**

<!-- Three lines each: the post, both labels, and who you think is right and
     why — grounded in the staff definitions you were both applying.

     Then sort each into one of three piles:
       (a) the rule covered it and I applied it loosely → a consistency problem
       (b) the rule genuinely doesn't say               → a gap in the definitions
       (c) the rule is ambiguous here and my reading is defensible → argue it.
           This is a legitimate win.

     Pile (a) is the one that matters most for your diagnosis: if you applied a
     written rule two different ways on 30 posts, that is direct evidence about
     what you did across your own 200. -->

**1.** (sp_003)
> *The post:* "The club championship scoring changed in 2019 from top-6 to top-10. Since then our B team has finished above the A team twice. That's not depth improving, it's the scoring rewarding turnout."
>
> *Staff said / I said:* `analysis` / `hot_take`
>
> *My call, and why:* Staff is right. The post gives a named date (2019), a named rule change (top-6 to top-10) and a named result (B team above A team twice). The conclusion only works because of the rule change, so under rule 1 the fact is load-bearing. I let the confident "That's not X, it's Y" ending make it sound like a hot take. Rule 2 says strength of feeling isn't support, and the reverse holds too: a confident tone doesn't cancel the support that's there.
>
> *Which pile:* (a), a consistency problem

**2.** (sp_004)
> *The post:* "Everyone blames the hill at 18 miles. I split the field into people who ran the first half under 1:45 and over, and the slowdown after 18 was almost identical for both groups. If the hill were the problem the fast starters would fall apart harder."
>
> *Staff said / I said:* `analysis` / `hot_take`
>
> *My call, and why:* Staff is right. The writer sets up a test (splitting the field at 1:45), reports what it showed (almost identical slowdown) and draws the inference from it. That is the kind of argument the `analysis` definition describes. I think the "Everyone blames..." opening read to me as a contrarian claim, and I labelled the framing instead of the argument.
>
> *Which pile:* (a), a consistency problem

**3.** (sp_005)
> *The post:* "Carbon plates aren't the whole story. My times dropped 2% in the shoes and another 2% the following year in the same pair, when the only thing that changed was going from 35 to 50 miles a week."
>
> *Staff said / I said:* `analysis` / `hot_take`
>
> *My call, and why:* Staff is right, though this one is genuinely borderline (staff flagged it HARD). The first sentence is an unsupported hot take on its own. But the second sentence carries the post: two comparable 2% drops, with mileage as the only variable that changed. Rule 1 asks whether the fact carries the argument, not whether the sample is big enough, and here it does. Rule 4 points the same way, because the post spends most of its words on the numbers.
>
> *Which pile:* (a). The case for my label only covers the first sentence, so it isn't defensible as (c).

**4.** (sp_006)
> *The post:* "Checked the entry lists. 41% of this year's field have never run the distance before, against 26% five years ago. That's why the finish-line photos look different, not because standards dropped."
>
> *Staff said / I said:* `analysis` / `hot_take`
>
> *My call, and why:* Staff is right, and this is the clearest miss of the six. The post has two checkable percentages, and they're used to reject a rival explanation ("not because standards dropped"). This is almost exactly the rule 1 `analysis` example. The "That's why..." ending is confident, but that confidence comes from the numbers.
>
> *Which pile:* (a), a consistency problem

**5.** (sp_010)
> *The post:* "Three of us ran the same session on the same day, different shoes, within 10 seconds of each other over 5 miles. I'm not saying shoes do nothing, but whatever they do was smaller than the noise between three people."
>
> *Staff said / I said:* `analysis` / `hot_take`
>
> *My call, and why:* Staff is right. I marked it down because three runners on one day is weak evidence. But the `analysis` definition asks for a fact that is specific, checkable and doing work, not for strong evidence. "Within 10 seconds over 5 miles" is checkable, and the claim (shoe effect < noise) rests entirely on it. The writer even hedges, which a hot take doesn't do. I was grading how good the evidence was when the rule only asks whether it's there and load-bearing.
>
> *Which pile:* (a), a consistency problem

**6.** (sp_029)
> *The post:* "Just realised the shoes I set every PB in this year are the ones I bought by accident in the wrong size."
>
> *Staff said / I said:* `reaction` / `analysis`
>
> *My call, and why:* Staff is right. It contains a checkable fact (the shoes are the wrong size), but `analysis` has to *make an argument*, and this post doesn't argue anything. It reports the writer's own realisation from just now ("Just realised"), which is the `reaction` definition. Under rule 3, a fact only promotes a post to `analysis` when it is load-bearing in an argument, and here there is no argument for it to carry. I think I over-corrected on this one after realising late that I'd been too stingy with `analysis`.
>
> *Which pile:* (a), a consistency problem

**What the pattern in my disagreements tells me:**

All six disagreements are on staff's side, and five of the six go the same way:
real `analysis` labelled `hot_take`. Overall I gave out 6 `analysis` labels
against staff's 10 and 15 `hot_take` against their 10. I had no disagreements
on the `reaction` vs `hot_take` boundary. So my problem isn't that the
definitions are unclear. I applied rule 1 more strictly than it is written in
two specific ways:

1. **I let tone override content.** Every one of the five misses has a
   confident or contrarian frame ("That's not X, it's Y", "Everyone blames…",
   "aren't the whole story"). I labelled the frame and ignored the fact
   underneath it.
2. **I graded the quality of the evidence instead of whether it was present
   and load-bearing.** Small samples (n=1, n=3) and the writer's own data got
   marked down, even though the definition counts "a stat, a date, a time" as
   support.

None of these are gaps in the definitions (pile b), and none of my labels hold
up as a defensible alternative reading (pile c). They are all pile (a). That
matters for my own 200 labels, because it's direct evidence that I let the
surface feel of a post decide when a written rule asks about its structure. My
own hardest rule is the same kind of proportional judgement ("does the
commenter's story take up more of the comment than the words aimed at OP?"),
and my own posts were AI-pre-labelled and then checked. If I made this
tone-over-structure mistake on 30 posts with the rules in front of me, I
probably made it on some of the `anecdote`/`support` boundary too: a warm,
supportive opener could have pulled a mostly-story comment into `support`. That
would fit the confusion matrix, where all 5 real `anecdote` posts were predicted
`support`. Part of that collapse may be a labelling consistency problem, not
only a model problem.



---

## The Improvement

**What I changed:** One training setting: `EPOCHS` went from 3 to 10 in section
2 of the notebook. Everything else is unchanged: same 150 labels, same learning
rate (2e-5), batch size (16), seeds (42, 7, 2024) and splits. The re-run was
saved with `RUN_LABEL = "after"` to `results_three_seeds_after.json`.

**Which diagnosis pointed at it:** Misses 1 and 2. On seeds 42 and 7 the
model predicted `support` for all 23 test posts. Those two seeds gave identical
results, which looks like a model that never trained long enough to leave the
majority class, not one confused by a boundary. Three epochs of about 104 posts
at batch size 16 is only 21 updates. The zero-shot baseline showed that
`anecdote` and `pushback` can be found from the text, so I tested whether the
model just needed more training before blaming the labels. I picked this over
adding 30 `pushback` posts because that would mean collecting new comments,
and over relabelling because my agreement report made labelling the
*secondary* suspect.

### Run Log — After

| Criterion | Target | Seed 42 | Seed 7 | Seed 2024 | Verdict |
|---|---|---|---|---|---|
| 1. Macro F1 | ≥ 0.45 | 0.483 | 0.746 | 0.503 | MET (was MISSED) |
| 2. `anecdote` F1 | ≥ 0.40 | 0.600 | 0.800 | 0.600 | MET (was MISSED) |
| 3. `pushback` recall | ≥ 0.50 | 0.00 (0/3) | 0.33 (1/3) | 0.00 (0/3) | MISSED |
| 4. Agreement with staff labels | ≥ 75% | 80% | 80% | 80% | MET (unchanged; not affected by training) |
| 5. Confidence gap (top third − bottom third accuracy) | ≥ 0.40 | 0.571 | 0.286 | 0.429 | MISSED (was MET) |

| Measure | Seed 42 | Seed 7 | Seed 2024 | Spread |
|---|---|---|---|---|
| Overall accuracy | 0.739 | 0.870 | 0.783 | 0.130 |
| Macro F1 | 0.483 | 0.746 | 0.503 | 0.263 |
| F1 — `anecdote` | 0.600 | 0.800 | 0.600 | 0.200 |
| F1 — `pushback` | 0.000 | 0.500 | 0.000 | 0.500 |
| F1 — `support` | 0.848 | 0.938 | 0.909 | 0.089 |

Confusion matrix, seed 42 (after):

| true \ predicted | anecdote | pushback | support |
|---|---|---|---|
| **anecdote** | 3 | 0 | 2 |
| **pushback** | 1 | 0 | 2 |
| **support** | 1 | 0 | 14 |

**Did it help, and how do I know:**

Yes for `anecdote` and macro F1. No for `pushback`. It also broke criterion 5.

- **The collapse is gone.** Before, seeds 42 and 7 put all 23 posts in the
  `support` column. After, every seed predicts `anecdote` and catches 3–4 of
  the 5. Seed 42's matrix went from 0 / 0 / 5 to 3 / 0 / 2 on the `anecdote`
  row, and the model now makes mistakes in both directions (1 `support` called
  `anecdote`). Accuracy rose on every seed (0.652 → 0.739, 0.652 → 0.870,
  0.739 → 0.783). Changing only the epoch count fixed the anecdote problem, so
  the main cause of miss 2 was training length, not my labels.
- **`pushback` barely moved.** Only seed 7 caught one. The other `pushback`
  posts are now split between `support` and `anecdote` instead of all going to
  `support`. More training didn't fix it, which fits my diagnosis for miss 3:
  about 12 training examples, split across three different kinds of comment,
  isn't enough. Training longer can't create examples that aren't there.
- **Criterion 5 now misses, and seed 7 shows why.** Seed 7 is the best model
  (0.870 accuracy), but even its *least* confident third is 71% right, so the
  gap is only 0.286. The before-model passed this criterion by being useless
  (always `support`), and the better model fails it because it's right even
  when unsure. A gap measure punishes a model that is good everywhere. I'm
  leaving the criterion and its verdict as they are, because it can still be
  measured. But it's a sign that the gap number alone doesn't measure "useful
  confidence".
- **Caveat on stability.** Accuracy now spreads 0.130 across seeds (up from
  0.087), and the notebook flags anything over 0.10 as too unstable to trust.
  Seed 7 got lucky on its split. Criteria 1 and 2 are MET on all three seeds,
  but seeds 42 and 2024 clear macro F1 by only 0.03–0.05. Also, I chose 10
  epochs before looking at any results and didn't tune it. The validation loss
  on seed 2024 was lowest around epoch 5, so some of the extra epochs may be
  overfitting.



---

## What's Still Broken

<!-- For each criterion still missed: what you'd do, and why you stopped. -->



**The gap between what I meant my labels to capture and what the model
learned:**
<!-- Two sentences. Your confusion matrix is the evidence. -->



<!-- ═════════════════════════════════════════════════════════════════════

     SUBMISSION CHECKLIST — unit 5

       [ ] criteria.md has five numbered criteria, each naming a NUMBER
       [ ] Each has a reason underneath tied to your data or taxonomy
       [ ] labels.csv: at least 150 rows, text/label/note, ONE file not split
       [ ] No label above 70%
       [ ] All five unit 5 sections have real content
       [ ] Label Taxonomy includes the decision rule for your hardest boundary
       [ ] The Dataset includes three hard cases
       [ ] results.json and test_split.csv committed (the notebook does this)
       [ ] At least four new commits
       [ ] Repository URL submitted — WRITE IT DOWN

     SUBMISSION CHECKLIST — unit 6

       [ ] Baseline vs. Trained table, with your prediction written beforehand
       [ ] Run Log — Before, five criteria across three seeds
       [ ] Confusion matrix TYPED AS A MARKDOWN TABLE
       [ ] A verdict on every criterion
       [ ] A diagnosis for every miss, using the agreement report as evidence
       [ ] Agreement Report with every disagreement adjudicated
       [ ] One improvement, with Run Log — After
       [ ] What's Still Broken
       [ ] results_three_seeds_before.json, results_three_seeds_after.json,
           baseline_results.json and
           agreement_results.json committed
       [ ] At least four new commits
       [ ] The SAME repository URL as last unit

     Do not delete and recreate this repository.
     ═════════════════════════════════════════════════════════════════════ -->

---

📖 **How to run this project: [RUNNING.md](RUNNING.md)**
