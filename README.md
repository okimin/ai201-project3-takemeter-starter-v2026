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
| support | 67 | 65  |
| anecdote | 25 | 24 |
| pushback | 11 | 11 |
| **Total** | 103 | 100% |

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
| 1.  |  |  |  |  |  |
| 2.  |  |  |  |  |  |
| 3.  |  |  |  |  |  |
| 4.  |  |  |  |  |  |
| 5.  |  |  |  |  |  |

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
| 1 |  |  |  |  |
| 2 |  |  |  |  |
| 3 |  |  |  |  |
| 4 |  |  |  |  |
| 5 |  |  |  |  |

**Diagnoses**

<!-- For each miss: the cause, and how you know. The four common causes are:
     too few examples for a label, a boundary you applied inconsistently, a
     genuinely hard label pair, and a task the model can't reach from this
     much data.

     ⚠️ Use your agreement report as evidence. It is the only instrument you
     have that can tell a LABELLING problem from a MODEL problem, and this
     section is graded on whether you used it that way. -->



---

## Agreement Report

<!-- Your rate against the staff set, and every disagreement adjudicated.

     Remember you labelled these 30 under the STAFF taxonomy in
     data/staff_taxonomy.md, not your own — so every argument below is made
     from those definitions and those decision rules. -->

**Agreement rate:** ___ / 30 = ___%

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

**1.**
> *The post:*
>
> *Staff said / I said:*
>
> *My call, and why:*
>
> *Which pile:*

**2.**
> *The post:*
>
> *Staff said / I said:*
>
> *My call, and why:*
>
> *Which pile:*

**What the pattern in my disagreements tells me:**



---

## The Improvement

**What I changed:**

**Which diagnosis pointed at it:**

### Run Log — After

| Criterion | Target | Seed 42 | Seed 7 | Seed 2024 | Verdict |
|---|---|---|---|---|---|
| 1.  |  |  |  |  |  |
| 2.  |  |  |  |  |  |
| 3.  |  |  |  |  |  |
| 4.  |  |  |  |  |  |
| 5.  |  |  |  |  |  |

**Did it help, and how do I know:**

<!-- If it didn't, say so. Relabelling that didn't help is a genuinely
     interesting result and earns full credit. -->



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
