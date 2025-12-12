# Test Design Techniques Summary — My Understanding (EP, BVA, DT, STT)

## 1. Equivalence Partitioning (EP) 

**Definition**

EP is basically grouping input values based on how they behave in the system.
If a bunch of values give the exact same result, I don’t test all of them — I test just one from that group because the outcome will be the same for all.

**Why we use EP**

* Saves time when the range of inputs is huge
* Covers the functionality smartly with fewer test cases
* Avoids repeating the same test 100 times

**How partitions are formed**

Two values belong to the same partition ONLY if the system treats them the same way.

**Example:**
Password length must be 8 to 16 →

* Partition 1: valid (8–16)
* Partition 2: too short (<8)
* Partition 3: too long (>16)

**Examples**

Age must be 18–60

* <18 → invalid
* 18–60 → valid
* > 60 → invalid

Cart total must be 500–2000 for discount

* <500
* 500–2000
* > 2000

**Common mistakes testers make**

* Writing test cases instead of partitions
* Missing hidden rules (like uppercase, lowercase, special characters)
* Creating too many partitions for no reason
* Not checking for multiple conditions (ex: length + character rule)

**How to avoid mistakes**

* Always read the rule first, not the input
* Partition based ONLY on behavior
* Don’t overthink: if system treats a value differently → new partition
* Pick just one representative per partition

**When to use EP**

* Whenever input range is large
* Form validations (age, quantity, price, character limits, etc.)
* Business rules that depend on ranges

---

## 2. Boundary Value Analysis (BVA) [Image of Boundary Value Analysis]

**Definition**

BVA is checking the values that sit exactly at the edges of the rule — because this is where most bugs hide.
I test the lower boundary, upper boundary, and ±1 around them.

**Why BVA catches many bugs**

Because devs often misunderstand the rule or implement it incorrectly at the edges.
(Example:
“Less than 500” → does 500 count or not?
People mess this up all the time.)

**Classic BVA pattern**

If valid range is X to Y, I test:

* X
* X−1
* Y
* Y+1
* (one value in between)

**Examples**

Password length 8–16

* 7 → invalid
* 8 → valid
* 16 → valid
* 17 → invalid

Amount must be >0 (but system allows 0)

* 0
* 1
(Here Y is open-ended → only lower boundary matters.)

Cart quantity must be 1–5 (but 0 clears cart)

* 0 → allowed but not valid
* 1 → valid
* 5 → valid
* 6 → invalid

**Common mistakes testers make**

* Forgetting ±1 values
* Testing random middle values instead of edges
* Not clarifying inclusive/exclusive rules
* Confusing negative cases with partitions instead of boundaries

**How to avoid mistakes**

* Write boundaries clearly before selecting values
* Always ask: “Is the boundary included or excluded?”
* Don’t skip the +1 / −1 values

**When to use BVA**

* Range-based rules
* Min/max limits
* Input text lengths
* Numeric fields

---

## 3. Decision Table Testing (DT) 

**Definition**

DT is for testing logic — not values.
When multiple conditions decide an outcome, DT helps me list all combinations and see which ones lead to success and which fail.

I don’t care about the data here — I care about the rules.

**Why we use DT**

* Handles complex logic cleanly
* Makes missing combinations obvious
* Ensures every rule is covered

**Typical example**

Login logic:
If username = valid AND password = valid → login success
Anything else → fail

**Decision table:**

| Username | Password | Result |
| :--- | :--- | :--- |
| V | V | Success |
| V | I | Fail |
| I | V | Fail |
| I | I | Fail |

**Examples**

ATM withdrawal:
Conditions:

* Card valid
* PIN correct
* Balance enough
* ATM has cash

You create rows for every combination that matters.

Coupon application:

* Cart >= 999
* User logged in
* Coupon not expired
* User has not used coupon before

**Common mistakes testers make**

* Testing data instead of logic
* Missing combinations
* Not focusing on the final result (outcome)
* Overcomplicating the conditions

**How to avoid mistakes**

* Keep conditions simple (true/false)
* Only test combinations that matter
* Identify the core rule → derive outcomes

**When to use DT**

* Login flows
* Payments
* Coupon/discount logic
* ATM transactions
* Any “IF this AND this OR this THEN that” logic

---

## 4. State Transition Testing (STT) 

**Definition**

STT checks whether the system moves from one state to another the right way.
Same action can give different results depending on the state, so we test if the state flow is correct.

**Why we use STT**

* To ensure screens/pages behave correctly based on current state
* To catch invalid transitions
* To confirm system follows expected flow

**Examples**

Login session:
States: Logged Out → Logged In → Idle → Logged Out
Invalid example: Idle → Payment (not allowed)

Order flow:
Browsing → Add to Cart → Checkout → Payment → Order Placed
Invalid example: Browsing → Order Placed directly

**Real-case examples**

* ATM: Active → Locked after 3 wrong PIN attempts
* App session timeout: Active → Idle → Logged Out
* Multi-step forms: Step 1 → Step 2 → Step 3 (can’t jump to Step 3 directly)

**Common mistakes testers make**

* Testing screens instead of states
* Missing negative transitions
* Not mapping all states properly
* Assuming linear flow (not always true)

**How to avoid mistakes**

* Identify all states first
* Map valid transitions clearly
* Check for invalid transitions too
* Think like: “At this state, what SHOULD happen?”

**When to use STT**

* Login/session behaviors
* Checkout flows
* Multi-step processes
* Online ordering
* ATM flows
* Account lock/unlock logic

---

## ⭐ Final Quick Revision Table

| Technique | What it Tests | Why It’s Useful |
| :--- | :--- | :--- |
| EP | Groups of inputs | Reduces test count, smart coverage |
| BVA | Edges of valid range | Catches common boundary bugs |
| DT | Logical combinations | Ensures logic is correct |
| STT | System states & transitions | Validates flow and prevents invalid jumps |