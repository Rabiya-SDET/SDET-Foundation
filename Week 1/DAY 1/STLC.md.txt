STLC – How I Actually Handle Testing (QA + SDET Perspective)
STLC is just the structured way I handle testing from start to finish.
It makes sure I don’t miss requirements, I test in the right order, and the build actually goes out in a stable state.
It’s basically the flow I follow — understand the requirement, plan the approach, design the tests, set up the environment, execute, log defects, and close it cleanly.

Stages is Stlc(Add-to-Cart used as example throughout):

1. Requirement Analysis

This is where I make sure I know exactly what the feature is supposed to do.
If anything is vague, contradictory, missing, or untestable, I fix it here.

What I look for:

--Missing rules

--Edge cases the BA forgot to mention

--API contract gaps

--Data flow / DB changes

--Dependencies (inventory, pricing engine)

--Risks that might hit later

Example (Add-to-Cart):

--Confirm max quantity rules

--Clarify how price recalculates

--Ask what happens if stock changes mid-session

--Check cart persistence rules

--Validate API response fields (itemId, qty, subtotal)

Output:
Clear requirements, fewer surprises later, updated RTM.

2. Test Planning

Now I decide how I’m going to test the feature — scope, strategy, depth, tools, risks.

What I plan:

--What’s in scope / out of scope

--UI, API, DB coverage

--Test data strategy

--Automation candidates

--Risks and dependencies

--Entry/Exit criteria

Example:

--UI flow: Add → Update qty → Remove

--API flow: totals, discounts, price logic

--Data: in-stock, out-of-stock, discounted items

--Risk: inventory data delay breaking cart logic

Output:
A clear plan that removes confusion during execution.

3. Test Case Design

I convert requirements into actual coverage — not just steps.

What I design:

--Positive + negative + boundary cases

--Edge cases

--API validations

--Data variation

--BVA, EP, Decision table

--RTM updates

Example:

--qty = 1, 2, max, max+1

--OOS behaviour

--Price recalculation logic

--Cart persistence on login/logout

Output:
Full scenario coverage + test data ready.

4. Test Environment Setup

Before I test anything, I make sure the environment is stable.

What I check:

--Deployment successful

--Smoke test passes

--UI ↔ API aligned  

--Test data ready

--Console/network logs clean

Example:

--Product list loads

--Add-to-Cart API returns correct structure

--No 500/404 errors

Output:
Stable environment → ready for execution.

5. Test Execution

This is where I actually run tests and verify behaviour.

What I do:

--Functional + API + DB checks

--Validate business logic

--Capture logs, screenshots, API payloads

--Raise defects with proper evidence

--Retest fixes

--Partial regression as needed

Example:

--Update qty → API recalculates totals correctly

--Remove item → DB + UI sync

--OOS product → Add button disabled

Output:
Passed/failed results + defects logged.

6. Defect Logging & Tracking

A bug is useful only if it’s clearly documented.

My defect includes:

--Summary

--Steps

--Data used

--Expected vs actual

--Logs, screenshots, API responses

--Severity/Priority

--Environment

Output:
Clean defects dev can fix without guessing.

7. Test Closure

Final verification before sign-off.

What I confirm:

--Planned cases executed

--All major bugs resolved

--Regression completed

--Risks documented

--Test Summary Report prepared

--Go/No-Go recommendation

Output:
Clear closure + stable release.