# Client review: Larkspur disruption-care agent

**To:** Room 0  
**From:** Larkspur client review agent, on behalf of Priya Raghavan  
**Re:** the disruption-care agent you walked us through in our last session  
**Generated:** 2026-11-17 15:54

## Priya's note

> Our vendor says we should just be using your best model.
>
> Why aren't we?
>
> Priya Raghavan, Larkspur Airlines

She sent that before this session opened. She means it. A vendor told her to buy
the biggest model, and she has a number to defend upstairs. Her four questions from
day one are still open. Naming a model answers none of them.

## Still open from day one

| Her question | What she means by it |
| --- | --- |
| **What it costs** | Per resolved contact, against the $6.90 a human contact costs us. |
| **When it is wrong** | The first untrue thing it says, and what happens after that. |
| **Who runs it** | In June, after you have left. |
| **What you left out** | The scope you cut, and why. |

## What the review agent found

Larkspur pointed a review agent at your repository. It read the
code. It did not run your agent, and the only file it changed is this one. Each
item below names the file and the line it is about.

**1. agent.py search_alternatives description is now one sentence of 218 characters; the other 8 tool descriptions are unchanged shipped text.**

Your diff replaced "search" with "When the segment's disruption is established, use the information provided through the pnr to find rebooking options." It also names the return fields: flight numbers, date, seats available, excluded options with a reason, other cabin options. The traced run called next_available_day immediately before search_alternatives, and that tool is not among the nine schemas in build_tools().

Run python3 run.py --show-tools and paste the search_alternatives entry next to next_available_day.

**2. PITCH.md Number reads 61,102 to 56,038 tokens in across 5 tickets, and the repo holds no bench output that produced it.**

The only committed run is readout-trace.json: 17,346 tokens in, 4 API turns, 0 cache read, 0 written, hit ratio None. cache_control appears nowhere in agent.py. The pencil mark on TONE_ADDENDUM is still at 0 characters, and no diff line changes the system prompt. Your diff changes tool_use turns and one tool description, and nothing in the material shows which of those moved the total or by how much.

Run python3 bench.py --compare on your before and after labels and paste the full compare output.

**3. agent.py run_agent() was changed to append response.content and to read answer = text_of(response) after the loop ends.**

Before your diff the loop appended text_of(response) as the assistant turn, which drops tool_use blocks. It also overwrote answer on every iteration. Your version sends full content back, so tool_use_id values pair with tool_results(). MAX_TOOL_CALLS stays at 8 and the traced run used 4 turns, so nobody has seen the loop reach the cap.

Run python3 run.py --all --trace and paste the totals footer with the per-ticket API turns.

**4. No evals/cases.json exists, and PITCH.md Still broken names a failure that nothing in the repo reproduces.**

You wrote that two booking codes in one message makes the agent look up only the first. Neither run.py nor the traced run in readout-trace.json shows a two-PNR input. The banked gates are 1.2, 1.3, 1.4, 2.1, 2.2. Safety evidence is one trace line for K7PQ2M, and nothing yet covers confirm_rebooking without a token across other booking shapes.

Run python3 verify.py 4.1 and paste its output, then add a case with two PNRs to evals/cases.json.

**5. Your PITCH.md Lever line is still the template string cost | speed | intelligence, and agent.py has no knob that moves any of the three.**

TONE_ADDENDUM is empty, EXTRA_TOOLS is empty, and LOCAL_TOOLS has no executors. The traced run shows thinking seen on the wire: True with 14.0s wall clock and 1,174 tokens out. Priya's question about the best model has one answer if the lever is intelligence and another if it is cost, and nothing in your files says which one this build is.

Edit the Lever line in PITCH.md to one word and paste the bench-after figure that lever moved.

## Your four answers

The four lines under `## Priya asked` in your PITCH.md are still empty. They
are one line each and they are not a coding job: cost, what happens when it is
wrong, who runs it in June, and what you left out. Whoever on your side is not
editing agent.py is the right person to write them, and they are the four
things I will ask about first.

## Before our next meeting

> Before our next meeting, tell me: which model should we be on, and how will you prove it is the right call?
>
> Priya Raghavan, Larkspur Airlines

Bring two things. A recommendation, and the measurement behind it. If the model is
not the problem, say so, and bring the number that shows it.

## What this review read

- `agent.py (228 lines)`
- `PITCH.md`
- `TEAM.md`
- `readout-trace.json`
- `readout.html (evidence block)`
- given files that differ from the shipped pack: `verify.py`, `eval_harness.py`, `bench.py`, `readout.py`, `setup.py`, `pod_sync.py`, `run.py`, `review.py`, `support/__init__.py`, `support/client.py`, `support/data.py`, `support/models.py`, `support/tools.py`, `support/trace.py`, `support/offline.py`, `support/mock_backend.py`, `support/mcp_client.py`, `support/mcp_server.py`, `support/mcp_selftest.py`, `support/access.py`, `support/keyscan.py`, `support/review.py`

Reviewer: `claude-sonnet-5-5`. Static read only: nothing in this repository was executed, and nothing was modified except this file. Larkspur Airlines is a fictional training scenario. Confidential, do not distribute.
