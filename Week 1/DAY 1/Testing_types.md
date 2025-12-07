# Testing Types

## 1. Functional Testing

Functional testing is just checking whether the feature actually behaves the way the business wants. Not in theory — in reality.
I verify valid flows, invalid flows, edge cases, boundaries, and how UI/API/DB behave together.

**What I check:**

* Positive scenarios
* Negative scenarios
* Boundary values (min/max)
* Error messages & validations
* UI ↔ API ↔ DB consistency
* Business rules (price, qty, eligibility, stock)

**Add-to-Cart example:**

* Add 1 item → subtotal correct
* Increase qty → recalc price & discount
* Add beyond max → block + message
* Remove item → totals update
* UI details match API response → cart summary, qty, price

## 2. Smoke Testing

Smoke testing is my “Is this build even usable?” check.
If smoke fails → I stop. No point wasting 3 hours testing a broken build.

**What I check:**

* App loads
* Main screens open without crashing
* Core APIs respond (2xx)
* No major errors in network/console
* Navigation works (home → product → cart)

**Add-to-Cart example:**

* Product list loads
* Product detail opens
* Add to Cart button visible
* Cart API returns valid structure (not checking logic)

**Purpose:**
* If smoke passes → I start real testing.
* If smoke fails → send it back.

## 3. Sanity Testing

Sanity is a very small, laser-focused check after a bug fix or a minor code update.
I only test the exact area that changed.

**What I check:**

* The fix actually works
* The small area around it still behaves correctly
* No new side effects in the touched module

**Add-to-Cart example:**

Fix: subtotal not updating when qty changes.
Sanity:
* Change qty → subtotal recalculates
* Check boundary qty works
* Check UI/API return same value

(Not testing the entire cart → that’s regression.)

## 4. Regression Testing

Regression is where I confirm nothing old broke because of something new.
Any new change (feature or fix) can impact existing flows — directly or indirectly.

**What I check:**

* All core flows
* All impacted areas
* All major integrations
* Consistency of behavior across modules
* Business logic still holds
* No new defects introduced

**Add-to-Cart example:**

* After a discount logic update → I recheck:
* add → qty → remove
* pricing
* tax
* discount
* cart→checkout flow
* cart persistence
* inventory interactions
* Not because they changed directly — but because they easily break through dependencies.

## 5. Integration Testing

Integration testing is checking whether connected modules/services actually work together.
A feature working individually means nothing if the combined flow fails.

**What I check:**

* UI ↔ API data flow
* API ↔ DB updates
* Service A ↔ Service B communication
* Payload structure & response mapping
* Error propagation between layers

**Add-to-Cart example:**

UI sends qty update → API responds with recalculated totals → DB stores updated cart → UI displays correct subtotal
* If any layer breaks → integration is broken.

## 6. System Testing

System testing is the full end-to-end check of the entire application.
All modules, all integrations, all flows — as ONE system.

**What I check:**

* Complete workflows (Add-to-Cart → Checkout → Order Confirm)
* Cross-module consistency
* Data flow across UI/API/DB
* Business logic across the whole system
* Realistic user-level behavior

**Add-to-Cart example:**

* Add → edit → remove → checkout → payment → order
* Verify stock updates
* Verify orders appear in history
* Verify email/SMS triggers
* System testing = “Does everything work as a whole?”

## 7. UAT (User Acceptance Testing)

UAT is not about bugs — it's about “Does this make sense to the business?”
Stakeholders check whether the product aligns with business goals.

**What I check/prepare:**

* Scenarios in business language
* Data to demonstrate real user behavior
* Anything that impacts business flow
* Anything that feels confusing, even if technically correct
* Compatibility with business expectations

**Add-to-Cart example:**

Business verifies:
* Discount rules match their strategy
* Stock rules reflect real inventory logic
* Cart behavior is user-friendly
* No confusing steps or delays

## 8. Exploratory Testing

Exploratory is where I test without a script — using logic, experience, and curiosity.
This is where real bugs show up.

**What I check:**

* Edge cases that no one wrote down
* Weird user behavior
* Unexpected sequences
* UI glitches
* Timing issues and race conditions
* Sessions, refreshes, rapid clicks, etc.

**Add-to-Cart example:**

* Add → remove → add again quickly
* Switch accounts mid-cart
* Add while stock drops to 0
* Rapidly changing qty
* Network slow/interrupted
* Exploratory = finding bugs no document predicts.

---

##  NON-FUNCTIONAL TESTING

This is everything that’s not about “does it work,” but “how well does it work.”

### 9. Performance Testing

How fast does the system respond under load?

**Types:**

* Load (normal traffic)
* Stress (beyond limits)
* Spike (sudden jumps)
* Endurance (long duration)

**Add-to-Cart example:**

* 500 users adding items simultaneously
* Cart API time under pressure
* DB write speed under load

### 10. Security Testing

Ensuring the app is safe from attacks.

**What I check:**

* Authentication
* Authorization
* Session handling
* SQL injection
* Broken access control
* Sensitive data exposure

**Add-to-Cart example:**

* User cannot modify price through API
* Cart belongs only to that user
* No direct DB-facing parameters

### 11. Usability Testing

Checking how simple and intuitive the app feels to the user.

**What I check:**

* UI clarity
* Navigation
* Error messages
* Accessibility
* User effort required

### 12. Compatibility Testing

Ensuring the app works across:

* Devices
* Browsers
* OS versions

### 13. Reliability / Stability Testing

Ensuring the system behaves consistently over long periods or repeated actions.

---

##  FINAL SUMMARY

* **Functional** = does it work?
* **Smoke** = is it even testable?
* **Sanity** = did the fix work?
* **Regression** = did anything old break?
* **Integration** = do modules talk properly?
* **System** = does the whole app work end-to-end?
* **UAT** = does the business accept it?
* **Exploratory** = what breaks when I think like a real user?
* **Non-functional** = how well does the system perform, scale, behave, and secure itself?
