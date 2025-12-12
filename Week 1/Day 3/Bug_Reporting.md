# 📝 What is Bug Reporting?

Bug reporting is basically telling the dev team what broke, where it broke, and how they can see it break again.
Nothing fancy — just clean, clear communication.
If the bug report is confusing, devs will waste time, testers will waste time, and the fix will bounce back and forth.

My only goal when I raise a bug is: “Can the developer understand this in one read and reproduce it in one try?”

---

## 2. Why bug reporting matters

* Helps dev fix the issue fast
* Prevents rework and back-and-forth
* Keeps the sprint clean
* Acts as proof that functionality didn’t meet requirement
* Helps QA track regressions & retesting

A badly written bug report slows down the entire team.

---

## 3. What I ALWAYS include in a bug

I write bugs very practically.
My structure: 

**✔ Title (straight to the point)**

I never write novel titles.
It should tell the issue in one line.

Example:
“Cart subtotal not updating when qty increases from 1 → 2.”

**✔ Environment**

Where I saw the bug.

* QA / UAT / Prod
* Device/browser
* API version / UI version

**✔ Preconditions**

Any setup needed.
Example: “User must be logged in with at least 1 item in cart.”

**✔ Steps to Reproduce**

I keep this crisp:

1. Login
2. Add any item to cart
3. Increase qty from 1 → 2
4. Observe subtotal

**✔ Actual Result**

What the system did (wrong).
Example:
Subtotal stays the same.

**✔ Expected Result**

What it should have done.
Example:
Subtotal should update based on unit price × new qty.

**✔ Screenshots / Video / API logs**

I always attach proof.
No proof → dev thinks “works on my machine”.

**✔ Severity & Priority**

I decide based on impact:

* **Severity** = how bad the bug is
* **Priority** = how soon it should be fixed

Example:
Subtotal wrong → High Sev, High Priority (because pricing is critical)

**✔ Modules Impacted**

Very important for SDETs.

Example:
Cart → Checkout → Price Engine → Order Summary.

---

## 4. What mistakes testers usually make

This is where most juniors fail. I consciously avoid these:

❌ **Writing vague titles**

Wrong: “Cart not working”
Correct: “Subtotal not recalculated when qty increases from 1→2.”

❌ **Missing repro steps**

If a dev cannot reproduce, the bug is useless.

❌ **Not attaching evidence**

Screenshot + console logs + API payloads → non-negotiable.

❌ **Writing Expected Result like a story**

Expected should be ONE clean line.

❌ **Blaming dev or requirement**

Bug report is not for “who made the mistake”.
It is for “what is wrong”.

❌ **Marking everything as high severity**

Looks childish and gets ignored later.

---

## 5. Good VS Bad Bug Example (my tone)

❌ **Bad bug:**

Cart price wrong. Please fix ASAP.

✔ **Good bug:**

**Title:** Subtotal not updating when qty increased from 1→2 in Cart.

**Env:** QA env 1 | Chrome 119 | API v2.3

**Steps:**
1. Login
2. Add any item to cart
3. Increase qty from 1 to 2
4. Observe subtotal

**Actual:** Subtotal stays the same.
**Expected:** Subtotal = unit price × updated qty.

**Impact:** Affects cart → checkout → order summary.
**Severity:** High | **Priority:** High

**Attachments:** screenshot + API response (cart/summary)

---

## 6. Severity vs Priority (my tone) 

**Severity → How big the damage is**

* **Sev 1:** App crash, security issues, price calculation wrong
* **Sev 2:** Major functionality broken
* **Sev 3:** Minor issue
* **Sev 4:** UI alignment / cosmetic

**Priority → How soon it should be fixed**

* **P1** = Fix now
* **P2** = Fix in sprint
* **P3** = Fix later
* **P4** = Enhancement

I don’t confuse these.
Example: UI misalignment → Low Sev, Low Pri
Wrong pricing → High Sev, High Pri

---

## 7. When I raise a bug vs when I DON’T

**✔ Raise a bug if:**

* Requirement clearly says X but system does Y
* System breaks previous functionality
* Wrong data (UI/API/DB mismatch)
* Crash / freeze / major delay
* Logical errors (price, qty, stock, validation rules)

**❌ I don’t raise a bug when:**

* Requirement is unclear → clarify first
* Dev environment is unstable → check smoke
* Data issues in test data setup
* Expected behavior is misunderstood

---

## 8. My quick mental checklist before raising a bug

1. Am I 100% sure this is not a data issue?
2. Did I check logs / API / console?
3. Did I retest once more?
4. Did I verify this on another browser/device?
5. Do I have a clean screenshot/video?
6. Is my expected result based on requirement, not assumption?

If all yes → raise bug.

---

## 9. Very common real-time bugs in Login / Cart / Checkout

Just keeping this list helps you prepare for interviews.

**Login**

* Wrong validations
* Username case sensitivity issue
* Login success but token not stored
* Login API 200 but UI shows “error”

**Cart**

* Subtotal mismatch
* Item not removed
* Quantity update not reflected
* Price not recalculated
* API & UI mismatch

**Checkout**

* Address not saved
* Payment API fails but UI shows success
* Discount applied incorrectly
* Tax calculation wrong

---

### final one-line definition

Bug reporting is just me telling the dev exactly what broke, how I made it break, and giving them enough proof so they can fix it without guessing.