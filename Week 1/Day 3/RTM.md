# RTM — Requirement Traceability Matrix

## 1. What is RTM 

RTM is basically a mapping sheet that shows:

* every requirement
* which test cases cover that requirement
* and whether we missed anything

The whole point is simple:
Nothing should slip. If there is a requirement, it must have a test case.

This is how we prove to business that we actually tested everything they asked for.

---

## 2. Why we need RTM

* To make sure no requirement is left untested
* To quickly catch gaps
* To track changes when requirements get updated
* To avoid testing old or outdated flows
* To show clean coverage during release time

RTM is literally the easiest way to see whether we are “done” or not.

---

## 3. What an RTM usually contains

* Requirement ID
* Requirement description
* Test case IDs mapped to it
* Status (Covered / Missing / Outdated / Updated)
* Notes if requirement changed in sprint

It doesn’t need to be fancy — just clean and clear.

---

## 4. How I maintain RTM in Agile (the practical way)

Agile keeps changing requirements every sprint, sometimes mid-sprint.
So RTM will become useless if we don’t update it properly.

When a requirement changes, I update RTM in this order:

**(1) Update the requirement description first**

This is the main thing.
The old description is NOT valid anymore, so the RTM must reflect the new version.

**(2) Mark the old requirement as “Outdated” or “Revised”**

I don’t delete anything — I simply mark it outdated and keep the reference.
This helps during audits and tracking.

**(3) Add the new requirement ID or version**

Either I:

* create a new requirement ID, OR
* append a version like R01 → R01_v2

Depends on the team style, but the idea is:
old requirement ≠ new requirement
So they should not be mixed.

**(4) Update the mapped test cases**

* If old test case is no longer valid → mark “Not Needed / Expired”
* If requirement changed → new test cases must be written
* If old test case can still be reused → just remap it

Nothing fancy. Just keep the mapping correct.

---

## 5. What I DO NOT update (and why)

❌ **I do NOT update:**

* “Reason for change”
* “Business justification”
* “Who changed it”
* Long explanations about why the requirement changed

**Why?**
Because RTM is NOT a document to store history.
RTM is just a map between requirements and test cases.
Tracking reasons belongs in JIRA, not RTM.

If you clutter RTM with unnecessary info, it becomes unusable.

---

## 6. What testers usually do wrong (and how to avoid it)

❌ **Mistake 1: Forgetting to update RTM when requirement changes**

This leads to outdated test cases covering outdated requirements.

**Fix:**
RTM gets updated immediately when requirement changes — not during execution.

---

❌ **Mistake 2: Test cases mapped to wrong requirement**

Happens when testers hurry.

**Fix:**
Always double-check requirement ID before writing a test case.

---

❌ **Mistake 3: No mapping at all**

Some requirements never get mapped — huge red flag during release.

**Fix:**
Use “Missing” tag in RTM until test case is written.

---

❌ **Mistake 4: Mixing old and new requirement in same row**

This causes confusion.

**Fix:**
Old = Mark outdated
New = Add new row or new version

---

## 7. When do we use RTM?

* Before test design → to see which requirements need how many test cases
* During execution → to track coverage
* After requirement changes → to update mappings
* Before release → to prove full coverage to business

RTM is mostly about traceability, nothing else.

---

## 8. Small practical example (Login) 

| Requirement ID | Description | Test Cases | Status |
| :--- | :--- | :--- | :--- |
| R01 | User must login with email + password | TC01, TC02, TC03 | Covered |
| R02 (Old) | Login with OTP | TC04 | Outdated |
| R02\_v2 | Login with OTP + Rate Limit + Resend Flow | TC05, TC06 | Updated |
| R03 | Lock user after 5 failed attempts | Missing | TC pending |

This is how a clean RTM looks.

---

## 9. Summary

RTM is just a clean mapping between requirement ↔ test cases.
That’s it.

If a requirement changes → I update the description first, mark old one outdated, remap test cases, and write new ones if needed.

If a requirement is missing test cases → I mark it as Missing and create test cases for it.

The whole idea is simple: No requirement should go to production without proper test coverage.