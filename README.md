# The Unofficial Guide

Sruthika B — `campus_life` corpus

> **This file is your submission.** Fill it in as you go — most sections get
> written during the milestone that produces them, not at the end.
>
> How the starter works, and every command you'll need, is in `RUNNING.md`.
> Leave that file alone.
>
> **Paste everything as text.** No screenshots, no video. A typed table gets
> full credit; a picture of the same table gets none.
>
> Delete these instruction blocks as you replace them. The `<!-- -->` comments
> are notes to you and don't show up when the page renders — you can leave them
> or remove them.

---

# Unit 1

## What This Does

This system answers focused questions about campus life using the `campus_life`
corpus. The documents cover administrative policies, course workloads, dining,
housing, parking, and student advice. A question is matched to retrieved source
documents, and the generated answer is expected to identify the source it used.
Questions outside the corpus are refused when the relevance gate finds no close
enough match.

## Chunking Strategy

**Chunk size:** 800 characters maximum
**Overlap:** 0 characters

The corpus contains 88 short, focused documents averaging about 317 characters,
so each document can usually remain one self-contained chunk. The custom
`chunker.py::split_documents` function keeps headings with their content,
groups paragraphs up to 800 characters, and splits an oversized group at
sentence boundaries. After chunking, there are 88 chunks averaging 317
characters, with a shortest chunk of 178 and a longest of 549. I chose no
overlap because these short documents already preserve their context within one
chunk.

<!-- What about YOUR documents made you pick these numbers? Short posts and
     long sectioned guides don't want the same chunking, and "800 seemed
     reasonable" earns nothing. Point at something you noticed when you read
     the documents in Milestone 1.

     If you changed your mind partway through, say so and say why. That's worth
     more than pretending you got it right first time.

     Milestone 3. -->

## Sample Chunks

<!-- Five chunks, pasted as text. Label each one and name the file it came from
     AND the function that produced it — the grader checks your code against
     what you claim here.

     `python app.py chunks -n 5` prints all three for you. Copy them straight
     across.

     Milestone 3. -->

**Chunk 1** — source: `admin_add_drop_deadline.txt#0` — produced by: `chunker.py::split_documents`

```
On the add/drop deadline

You can add a course through the end of the second week. Dropping is a longer
window — through the end of week six — but a drop after week two shows as a W on
your transcript. Nothing anywhere on the registrar's site says this plainly, and
students find out from each other.
```

**Chunk 2** — source: `course_biol_160.txt#0` — produced by: `chunker.py::split_documents`

```
BIOL 160 Cell Biology

I lived here my sophomore year. Format is lecture three times a week with a
weekly lab. Assessment: four unit tests and a cumulative final. Not curved.

Expect 9 to 11 hours a week, the heaviest first-year course by reputation.

The one piece of advice: the unit tests come fast, roughly every three weeks;
falling behind once is very hard to recover from.
```

**Chunk 3** — source: `course_hist_118_workload.txt#0` — produced by: `chunker.py::split_documents`

```
Workload for HIST 118 Modern World History

People keep asking so: a lot of reading, about 120 pages a week, but no problem
sets. That's real time, not optimistic time.

It's front-loaded — the first month is heavier than the rest, partly because
you're learning the format.
```

**Chunk 4** — source: `dining_pellew_dining_hall_followup.txt#0` — produced by: `chunker.py::split_documents`

```
Re: Pellew Dining Hall

Adding to what people have said about Pellew Dining Hall. The wait figure of 12
to 18 minutes at peak matches what I've seen. If you're trying to eat between
classes, go before 11:45 and it's a different building entirely.

Also worth saying: the furthest hall from anywhere, next to the athletics centre.
Nobody tells you this at orientation.
```

**Chunk 5** — source: `housing_innisfree_hall.txt#0` — produced by: `chunker.py::split_documents`

```
Innisfree Hall — what it's actually like

Transferred in last year, so take this with a grain of salt. Built 1991,
renovated 2022. Rooms are doubles arranged as pairs sharing one bathroom between
two rooms.

The good: the shared-bathroom-between-two-rooms arrangement is the best compromise
on campus.

The bad: no air conditioning, which matters for the first three weeks of September.

Laundry costs $1.75 wash, $1.75 dry, app-based. On noise: moderate; the building
is L-shaped and the short wing is much quieter.
```

## Sample Answer

<!-- One complete question and answer, pasted as text, with the source line
     visible. Milestone 4. -->

**Question:**

**Answer:**

```
```

**My relevance cutoff:**

<!-- The number you set in config.py, and how you got there.

     You ran five questions your corpus covers and the five in OUT_OF_SCOPE
     that it clearly doesn't, and wrote down the best distance for each. What
     did those two groups look like? Where was the gap? Put the actual numbers
     here — the table below wants all ten rows.

     Milestone 4. -->

| Question | In corpus? | Best distance |
|---|---|---|
|  |  |  |

## How I Used AI

<!-- Two specific moments. For each: what you asked for, what came back, and
     what you changed about it.

     "I asked Claude to write the chunking function from my notes. It ignored
     the overlap, so I added that myself" is the level of detail we're after.
     "I used AI to help me code" is not.

     Milestone 5. -->

**1.** I used an AI self-check to pressure-test the five acceptance criteria. It
checked whether each criterion named a number or observable outcome, could be
tested by a stranger, and would be scored consistently. Based on that review, I
rewrote the chunk criterion from a subjective “complete idea” test to counting
whether 4 of 5 sampled chunks end at sentence or paragraph boundaries.

**2.** I asked AI to help reason about the corpus shape before implementing the
chunker. The useful conclusion was that `campus_life` contains short,
topic-focused documents, so paragraph-preserving chunks fit better than generic
fixed windows. I implemented and tested `chunker.py::split_documents` myself;
it keeps headings with content and produced 88 chunks averaging 317 characters.

<!-- ── Stretch features ─────────────────────────────────────────────────────
     Doing one? Say so here BEFORE you start. A feature this README never
     claims earns nothing.
     ───────────────────────────────────────────────────────────────────────── -->

---

# Unit 2

<!-- These sections get ADDED to what's already above. Don't delete or rewrite
     unit 1 — the point is that someone can see what you said before you knew
     how it went. -->

## Run Log — Before

This run was produced by `run_eval.py::main` and saved in `results/run_2026-09-27_2335.md`.

| Criterion | Target | Run 1 | Run 2 | Run 3 | Verdict |
|---|---|---|---|---|---|
| 1. Retrieved chunk contains the answer | 4 of 5 | 5 of 5 | 5 of 5 | 5 of 5 | MET |
| 2. Every answer names a source | 5 of 5 | 5 of 5 | 5 of 5 | 5 of 5 | MET |
| 3. Gate stops out-of-corpus questions | 4 of 5 | 5 of 5 | 5 of 5 | 5 of 5 | MET |
| 4. In a sample of 5 chunks, at least 4 should end at a sentence or paragraph boundary rather than splitting a sentence across two chunks. | 4 of 5 | — | — | — | not measured in this run |
| 5. At least 4 of the 5 answers should cite the correct source document and use information that is actually supported by that document. | 4 of 5 | — | — | — | not measured in this run |

### Real output from the run

The run log is one row per question, and the criterion summary above is aggregated from those passes. These are the actual model outputs that were produced in the run file.

#### How are juniors and seniors ordered in the housing lottery? — run 1

- Best distance: 0.2250 (passed the gate)
- Sources retrieved: admin_housing_lottery.txt, admin_parking_permits.txt, advising_registration.txt, housing_old_brewhouse.txt, housing_tamsin_court.txt

```
Juniors and seniors are ordered by accumulated credit hours first, with a random tie-break used only when necessary (admin_housing_lottery.txt).
```

#### How are juniors and seniors ordered in the housing lottery? — run 2

```
Juniors and seniors are ordered by accumulated credit hours first, with ties broken randomly (admin_housing_lottery.txt).
```

#### How are juniors and seniors ordered in the housing lottery? — run 3

```
Juniors and seniors are ordered by accumulated credit hours first, with a random tie-break used for ties (admin_housing_lottery.txt).
```

#### Do dining dollars roll over from the spring semester to the following autumn? — run 1

```
No, dining dollars do not roll over from the spring semester to the following autumn, and whatever is left in May disappears.

Source: admin_dining_dollars.txt
```

#### Do dining dollars roll over from the spring semester to the following autumn? — run 2

```
No, dining dollars do not roll over from the spring semester to the following autumn; whatever is left in May disappears (admin_dining_dollars.txt).
```

#### Do dining dollars roll over from the spring semester to the following autumn? — run 3

```
No, dining dollars do not roll over from the spring semester to the following autumn; whatever is left in May disappears. This comes from `admin_dining_dollars.txt`.
```

#### How late can a student declare a course pass/fail, and what grade is needed for a pass? — run 1

```
A student can declare a course pass/fail as late as week eight. A pass requires a C- or better.

Source: admin_pass_fail_option.txt
```

#### How late can a student declare a course pass/fail, and what grade is needed for a pass? — run 2

```
A student can declare a course pass/fail as late as week eight. A pass requires a C- or better.

Source: admin_pass_fail_option.txt
```

#### How late can a student declare a course pass/fail, and what grade is needed for a pass? — run 3

```
A student can declare a course pass/fail as late as week eight. A pass requires a C- or better.

Source: admin_pass_fail_option.txt
```

#### How quickly do student permits for the west parking lots usually sell out? — run 1

```
Student permits for the west lots sell out in about three days (admin_parking_permits.txt).
```

#### How quickly do student permits for the west parking lots usually sell out? — run 2

```
Student permits for the west lots sell out in about three days (admin_parking_permits.txt).
```

#### How quickly do student permits for the west parking lots usually sell out? — run 3

```
Student permits for the west lots sell out in about three days (admin_parking_permits.txt).
```

#### What must be done before registering, and how far ahead should students book an adviser appointment? — run 1

```
You need your adviser hold lifted before you can register, and students should book an adviser appointment two weeks out.

Source: advising_registration.txt
```

#### What must be done before registering, and how far ahead should students book an adviser appointment? — run 2

```
You need to have your adviser hold lifted before you can register, and you should book your adviser appointment two weeks out.

Source: *advising_registration.txt*
```

#### What must be done before registering, and how far ahead should students book an adviser appointment? — run 3

```
Before registering, you need to have your adviser hold lifted. Students should book an adviser appointment two weeks out.

Source: advising_registration.txt
```

### Relevance gate on out-of-corpus questions

Produced by `run_eval.py::check_out_of_scope`, cutoff 0.6. Refused 5 of 5.

| Out-of-scope question | Best distance | Gate |
|---|---|---|
| What is the capital of Mongolia? | 0.825 | refused |
| How do I change the oil in a diesel engine? | 0.934 | refused |
| Who won the 1994 World Cup? | 0.886 | refused |
| What is the recommended dosage of ibuprofen for a headache? | 0.844 | refused |
| How do I write a for loop in Rust? | 0.896 | refused |

## Verdicts

| # | Criterion | Verdict | How I decided |
|---|---|---|---|
| 1 | Retrieved chunk contains the answer | MET | All five in-scope questions passed in all three runs, so the target of 4 of 5 held. |
| 2 | Every answer names a source | MET | Every answer in the output names a source document, and the run log shows 5 of 5 passes. |
| 3 | Gate stops out-of-corpus questions | MET | The gate refused all five out-of-scope questions at the 0.6 cutoff. |
| 4 | Chunk boundary criterion | not measured in this run | This run did not include a separate chunk-sample audit, so this criterion cannot be scored from the run log alone. |
| 5 | Correct-source support criterion | not measured in this run | The run log records answer success, but not a separate manual check that each cited source actually supports the answer. |

## Diagnoses

The first three criteria met their targets without any miss, so there is no stage-level diagnosis to report for those. The run was structurally successful: retrieval and generation were able to answer the in-scope questions and the gate rejected all five out-of-scope prompts.

The only missing evaluation is for criteria 4 and 5. Those are not failures in this run; they are unmeasured because the run output records pass/fail by question, not a chunk-boundary audit or a source-support audit. In other words, the run validated the retrieval-and-answer pipeline, but not the chunk-quality and source-trustworthiness checks from the original acceptance criteria.

## Expanded Second Run — Not Completed

After adding two harder in-scope questions, I attempted to run the expanded
question set with `python3 run_eval.py`. The second run did not complete: the
Google generation API returned `503 UNAVAILABLE` and reported that the model
was experiencing high demand. No completed answer results or evaluator scores
were produced for this attempt, so it cannot be treated as a scored run.

The two added questions were:

1. After week two, what appears on a transcript if a student drops a course?
2. When should students eat at Pellew Dining Hall to avoid the longest waits?

The terminal screenshot of the `503 UNAVAILABLE` error was supplied in the
conversation but is not present as an image file in this repository, so it is
not embedded here. The error is transcribed above; the screenshot can be added
here once it is available in the workspace.

<!-- For each miss: which stage caused it, and how. The stage alone isn't
     enough — you need the mechanism.

     Not a diagnosis: "Question 3 didn't work."
     A diagnosis:     "Question 3 asks about laundry costs. The answer is in
                       one sentence that got split across two chunks, so
                       neither chunk on its own contains it."

     The five stages: loading → chunking → embedding → retrieval → generation.

     Look for a pattern. If three misses all ask about numbers, that's one
     problem, not three.

     Missed nothing? Say so, then say honestly whether your targets were set
     low, and which one you'd tighten and to what.

     Milestone 3. -->

## The Improvement

**What I changed:**

**Why I picked it:**

<!-- Connect it to a specific diagnosis above in one sentence. If you can't,
     you picked a fix because it sounded impressive. -->

### Run Log — After

<!-- Same format, same five criteria, three runs each.
     `python run_eval.py --label after` -->

| Criterion | Target | Run 1 | Run 2 | Run 3 | Verdict |
|---|---|---|---|---|---|
| 1. Retrieved chunk contains the answer | 4 of 5 |  |  |  |  |
| 2. Every answer names a source | 5 of 5 |  |  |  |  |
| 3. Gate stops out-of-corpus questions | 4 of 5 |  |  |  |  |
| 4. | | | | | |
| 5. | | | | | |

**Did it help?**

<!-- Say plainly whether it did, and how you know. If it made things worse,
     say that — a change that backfired, honestly reported, earns full credit
     and is more interesting than one that worked. What matters is that you can
     tell.

     Milestone 4. -->

## What's Still Broken

<!-- For each criterion still missed after your fix: what you'd do about it,
     and why you stopped where you did.

     "I ran out of time" is fine if it's true. Pretending nothing is left is
     not.

     Milestone 5. -->

## What I'd Do Differently

<!-- Knowing what you know now — which of your five criteria would you write
     differently, and why?

     Milestone 5. -->
