# Reflection

Developed further: **city-explorer** — https://github.com/arobidepaul/city-explorer

<!--
Pointers below are starting material, not answers. Write these yourself,
same as problem.md. Delete this comment block once you've written your
answers.
-->

## 1. What did a fresh session get wrong or ask about that an earlier round had already settled? What was missing from the repository that would have prevented it?

<!--
Pointer: commit c153cb8 ("Replace synthetic grid with real Chicago street
data (R1, R6-R10)") built R8-R10 (Round 3's scope) in the same commit as
Round 2's R1/R6/R7, before Round 3's requirements existed in problem.md at
all, and bundled everything into one commit instead of small steps. It
also added zero decision records and no requirement-tagged tests for
R1/R6-R10 at the time -- fixed later in commit 020acfc
("Add missing tests and decision records for Rounds 2-3").

Separately, the Round 5, 6, and 7 sessions each independently decided "no
new decision record needed" (see handoff-round-5.md, handoff-round-6.md,
and handoff-round-7.md's "Decisions made this round" sections), reasoning
that their change was a structural copy of an earlier round's mechanism --
even though the assignment requires one every round regardless. Each gap
was filled after the fact: docs/decisions/0004, 0005, 0006.

What was missing from the repository: CLAUDE.md never stated a standing
rule like "a round's build must stay within that round's own requirement
list" or "write a decision record every round even if the mechanism
resembles an earlier one." Nothing in the repo would have caught either
pattern without an outside reviewer (me) checking the diff and git log
directly.
-->

## 2. In the round that changed an earlier requirement, what broke? Did the tests catch it, and does the decision record explain the change to someone who was not there?

<!--
Pointer: Round 2 changed R1 (problem.md line: "R1 (changed): The map
displays the real street layout of downtown Chicago..."). The entire
Round 1 city model broke: ROWS/COLS, blockId/parseBlockId, and the
grid-based street-name lookup in the original cityData.js were replaced
by SEGMENTS entirely. cityState.test.js's existing R2-R5 tests referenced
grid-cell ids and had to be rewritten against the new SEGMENTS array
(segmentA/segmentB/segmentC) in the same commit (c153cb8) as the
implementation change -- so there's no "test failed, then got fixed"
moment to point to; the rewrite happened in lockstep.

docs/decisions/0001-merge-street-segments-at-named-cross-streets.md
explains the core modeling choice (merging the raw dataset's node-level
breaks into one segment per named-cross-street block, and the Grant Park
drives special case). Read it and judge: does it actually explain the
change to someone who wasn't in the room, or does it assume context they
wouldn't have?
-->

## 3. Name one test that caught a real problem, or one test the assistant wrote that checked nothing useful. Quote it.

<!--
No node --test unit test is documented as having caught a real bug by
failing -- the two documented real catches were from manual/browser
testing instead: a CSS rule leaking into new filter buttons (fixed in
commit 9f21101, described in handoff-round-6.md) and a Playwright
viewport size issue (described in handoff-round-7.md, though that one was
a test-harness bug, not an app bug). You may want to look at those instead
of a unit test for this question, or go looking through
city-explorer/cityState.test.js yourself for one that either caught
something or is weaker than it looks.
-->

## 4. Choose one commit you would now write differently, and say how.

<!--
Strong candidate: c153cb8, "Replace synthetic grid with real Chicago
street data (R1, R6-R10)" in city-explorer. One commit did Round 2's work,
jumped ahead into Round 3's scope, and added Round 3's requirements text
to problem.md in the same commit as the code implementing it -- the
opposite of "requirements first."
-->

## 5. Choose one function in the project you developed further that you did not read while building it. Without an assistant open, read it and write what you think it does, in two or three sentences. Then ask an assistant, and say what you got right and wrong.

<!--
This one only works if you actually haven't read the function yet. Good
places to look if you're not sure what you skipped: city-explorer/app.js
has a fair amount of rendering code you may not have read line-by-line
(the overlap-avoidance logic around placedLabelRects, or the point-to-
polyline distance function used for click hit-testing, distanceToSegment).
Pick one, read it cold, write your guess, then ask.
-->
