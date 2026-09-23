# Acceptance criteria — The Unofficial Guide

Five criteria that say what "working" means for this system, written in unit 1
**before** any results existed.

An acceptance criterion names a target: a number, a count, a rate, or something
a person could plainly observe. *"Retrieval works"* is an opinion. *"For at
least 4 of my 5 test questions, the top results include a chunk containing the
answer"* is a criterion.

Under each one, write a sentence or two on **why that target** and not a
stricter or looser one. A reason that says something about your corpus or your
pipeline earns credit; *"80% seemed reasonable"* does not.

> Missing your own targets next unit costs you nothing. Setting a target so
> easy you can't miss it does.

---

## 1. Retrieved chunks contain the answer

For at least 4 of my 5 test questions, the top 5 retrieved chunks include at
least one chunk that contains the answer.

**Why this target:**
The answer has to be in the retrieval set before the model can answer well. In a
short factual corpus, one missing fact is enough to make a response wrong.

---

## 2. Every answer names a source

Every answer the system produces names at least one source document that was
actually retrieved for that question.

**Why this target:**
I want the answer to point back to something the system actually used. In this
corpus, weak or vague attribution is a common failure mode, so this is the
minimum grounding I need.

---

## 3. The relevance gate stops out-of-corpus questions

When I ask a question my documents clearly don't cover, the relevance gate
rejects it before generation and the system returns "I don't have enough
information about that" in at least 4 of 5 tries.

<!-- The five questions are the ones in `OUT_OF_SCOPE` at the bottom of
     `questions.py`, and `run_eval.py` puts them through the gate and writes
     what happened into your run log. Swap them for your own if you'd rather —
     just keep five of them, or the "4 of 5" above has nothing to be 4 of. -->

**Why this target:**
This is the guardrail against hallucinated answers. The corpus has a clear
in-corpus vs. out-of-corpus split, so the cutoff should be strict enough to
block off-topic questions without blocking the ones it can actually answer.

---

## 4. Chunks keep the important information together

For at least 4 of 5 sampled chunks, the text reads like a complete thought or paragraph, with no sentence cut off at either end.

**Why this target:**
These documents are short and factual, so the useful detail is often a single sentence or a very small paragraph. If a chunk breaks right through the middle of that fact, the retrieval system can still find it, but the answer becomes awkward or incomplete. I want the chunking to preserve the important idea most of the time, not just squeeze a few words into a fixed-size box.

---

## 5. The answer names the right place

For at least 4 of 5 test questions, the answer names the correct city or landmark from the corpus instead of drifting to a nearby but wrong location.

**Why this target:**
This corpus has a lot of places that are similar on the surface, so a wrong answer can sound believable even when it is not correct. I care about this because the point of the system is to help someone find the right local fact, and a wrong-location answer is more harmful than a clear refusal. This target is specific enough to measure, and it reflects the real risk in these documents.

---

<!-- ─────────────────────────────────────────────────────────────────────────
     UNIT 2 — read this before you change anything above.

     If a criterion turns out to be BROKEN rather than merely unmet, you can
     revise it, and that earns credit. But never delete or edit the original
     line. Add the revision underneath it, like this:

         ## 1. Retrieved chunks contain the answer

         For at least 4 of my 5 test questions, the retrieved chunks include
         one that contains the answer.

         **Why this target:** ...

         > **Revised in unit 2:** For at least 4 of 5 questions, the top three
         > results contain the answer.
         >
         > **Why revised:** I couldn't judge "the chunks include one that
         > contains the answer" the same way twice — I scored two questions
         > differently on Monday than on Wednesday. The new version is
         > something I can actually check.

     That's a revision because the criterion couldn't be MEASURED.

     Lowering a target because you missed it is not a revision, and it costs
     you the point:

         ✗ "I said 4 of 5 but got 2 of 5, so 2 of 5 is more realistic."

     A number you missed stays where it is, gets diagnosed, and gets a fix
     attempted. That's where the points are.

     The whole reason the originals stay visible is so someone can see what you
     said before you knew the answer.
     ───────────────────────────────────────────────────────────────────────── -->
