# Acceptance criteria — TakeMeter

Five criteria that say what "working" means for this classifier, written in
unit 5 **before** anything was trained.

**All five are yours this time.** None are given. You've had two projects of
practice.

An acceptance criterion names a number. *"The model is accurate"* is an
opinion. *"Every label has an F1 of at least 0.60 on the held-out set"* is a
criterion.

Under each, write a sentence or two on **why that number**. A reason that says
something about your data or your taxonomy earns credit — *"I picked 0.60 F1
for `reaction` because it's my smallest label and I only have about 50
examples of it"*. A reason that could be attached to any project does not.

> Missing your own targets next unit costs you nothing. Setting a target so
> easy you can't miss it does.

---

## Pick numbers you can defend

Not numbers that sound impressive. Three labels means a coin-flip guesser gets
about 33%, so a target of 0.40 is barely a target. Your number should sit
somewhere you'd honestly call useful.

**Cover at least three of these five areas.** They're here as prompts, not as a
form to fill in — a criterion that fits none of them is fine if it names a
number.

| Area | A question it could answer |
|---|---|
| Overall accuracy | How often does it need to be right to be worth using? |
| Per-label performance | Is one label allowed to be much worse than the others? |
| Balance | How lopsided can your label counts get before it's a problem? |
| Consistency | If someone else labelled the same posts, how often should you agree? |
| Confidence | Should a confident prediction be right more often than an unsure one? |

Two things worth knowing before you pick numbers, because both will affect
whether you hit them:

- **Your smallest label will have the jumpiest score.** If a label has 50
  examples, about 8 land in the test split. An F1 computed on 8 examples moves
  a lot between seeds. A target for that label should be looser than one for
  your biggest label, and saying so is a good reason.
- **Unit 6 tests across three seeds, and the target has to hold across all
  three.** A target of 0.65 against results of 0.71, 0.62, 0.68 is a **miss**.
  Pick with that in mind — it is stricter than it first sounds.

---

## 1. The model has to be fair to all three labels, not just `support`

Macro F1 is at least **0.45** on every seed (42, 7 and 2024).

**Why this target:**
Two-thirds of my comments are `support`, so a model can look fine on accuracy
just by saying "support" every time. That would get 10 of the 16 test posts
right while never once finding an anecdote or a pushback. Macro F1 counts each
label equally, so a model that only says "support" would score around 0.26.
0.45 means the model has to actually find some anecdotes and pushback instead
of hiding behind the big label.

---

## 2. It can tell a personal story apart from a supportive comment

`anecdote` F1 is at least **0.40** on every seed.

**Why this target:**
Support vs. anecdote is my hardest boundary. A lot of comments say something
nice to OP *and* mention the commenter's own boyfriend, and I had to lean on my
"which part is longer" rule to label them. There are only 4 anecdotes in the
test split, so I set this lower than I would for `support`. 0.40 roughly means
the model catches one or two of the four without calling everything an
anecdote.

---

## 3. It catches at least one of the two pushback comments

`pushback` recall is at least **0.50** (1 of the 2 test posts) on every seed.

**Why this target:**
Pushback is my smallest label, only 11 comments, and just 2 of them landed in
the test set. An F1 score on 2 posts would jump around between 0, 0.67 and 1.0
for no real reason, so I'm asking for the simplest honest thing: when someone
disagrees with OP, the model should notice at least half the time.

---

## 4. My own labels are consistent enough to trust

I agree with the staff labels on at least **75%** of the 30 posts in the
agreement check.

**Why this target:**
I used AI to pre-label my comments because of time, then went back and checked
them. That means I need some outside proof that my labelling is solid and not
just me agreeing with the AI. With three labels, random guessing gets about
33%, so 75% shows I'm applying written definitions the way someone else would.
If the model misses my other targets, this tells me whether the problem is the
model or my labels.

---

## 5. When the model is confident, it should actually be right more often

Accuracy on the model's most-confident third of the test posts is at least
**0.40 higher** than on its least-confident third, on every seed.

**Why this target:**
Each third is only about 5 posts, so 0.40 means at least two more correct
answers in the confident group, which is a gap big enough that it shouldn't
happen by luck. With this few test posts, one seed could show a big gap by
accident, which is why it has to hold on all three. If the confidence means
nothing, I can't use it to flag the tricky comments (the ones that are half
support, half story) for a human to double-check.

---

<!-- ─────────────────────────────────────────────────────────────────────────
     UNIT 6 — read this before you change anything above.

     If a criterion turns out to be BROKEN rather than merely unmet, you can
     revise it, and that earns credit. But never delete or edit the original
     line. Add the revision underneath, like this:

         ## 2. Every label performs acceptably

         The model performs well on all labels.

         **Why this target:** ...

         > **Revised in unit 6:** Every label has an F1 of at least 0.60 on
         > the held-out set.
         >
         > **Why revised:** "performs well" gave me nothing to check. I
         > couldn't produce a verdict from it at all.

     That's a revision because the criterion couldn't be MEASURED.

     Lowering a target because you missed it is not a revision, and it costs
     you the point:

         ✗ "Overall accuracy of at least 0.65" → "at least 0.55", because
            0.65 turned out to be optimistic for 200 examples.

     A number you missed stays where it is, gets diagnosed, and gets a fix
     attempted. That's where the points are.
     ───────────────────────────────────────────────────────────────────────── -->
