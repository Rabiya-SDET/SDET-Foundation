# Login Test Cases

## TC_ID: TC_LOGIN_POS_01

**Title:** Login with valid email and valid password — happy path
**Preconditions:** User account exists and active. Environment: QA, correct build deployed.
**Steps:**

1. Open Login page.
2. Enter email user1@example.com.
3. Enter password ValidPass123 (valid).
4. Click Login.

**Expected Result:** User is logged in and redirected to Home/Dashboard. No error shown.
**Test Data:** user1@example.com / ValidPass123
**Technique Used:** None (functional)

---

## TC_ID: TC_LOGIN_POS_02

**Title:** Login with valid email and password with leading/trailing spaces trimmed
**Preconditions:** Account exists. QA env.
**Steps:**

1. Open Login page.
2. Enter email user1@example.com (note spaces).
3. Enter password ValidPass123 (spaces).
4. Click Login.

**Expected Result:** Spaces trimmed, login succeeds, redirect to Dashboard.
**Test Data:** user1@example.com /  ValidPass123
**Technique Used:** EP (input normalization)

---

## TC_ID: TC_LOGIN_POS_03

**Title:** Login with valid email and password (remember me checked)
**Preconditions:** Account exists. Browser cookies enabled.
**Steps:**

1. Open Login page.
2. Enter valid credentials.
3. Check Remember me.
4. Click Login.
5. Close and reopen browser, navigate to app.

**Expected Result:** User stays logged in (or email pre-filled) as per product behaviour.
**Test Data:** user1@example.com / ValidPass123
**Technique Used:** None (functional)

---

## TC_ID: TC_LOGIN_POS_04

**Title:** Login using valid email and valid password after OTP disabled (API-only flow)
**Preconditions:** OTP flow disabled for user; API reachable.
**Steps:**

1. Open Login page.
2. Enter credentials.
3. Click Login.

**Expected Result:** Login succeeds; token issued; API /auth/login returns 200 with token.
**Test Data:** user2@example.com / ValidPass456
**Technique Used:** Integration (UI ↔ API)

---

## TC_ID: TC_LOGIN_POS_05

**Title:** Login with case-insensitive email (email lower/upper case)
**Preconditions:** Account exists (email stored lowercase).
**Steps:**

1. Enter User1@Example.com (mixed case).
2. Enter valid password.
3. Click Login.

**Expected Result:** Email treated case-insensitively, login succeeds.
**Test Data:** User1@Example.com / ValidPass123
**Technique Used:** EP (input normalization)

---

## TC_ID: TC_LOGIN_NEG_01

**Title:** Login with invalid password (valid email)
**Preconditions:** Account exists.
**Steps:**

1. Enter valid email.
2. Enter wrong password WrongPass.
3. Click Login.

**Expected Result:** Login fails. Show message: “Incorrect email or password.” No token issued.
**Test Data:** user1@example.com / WrongPass
**Technique Used:** None (negative)

---

## TC_ID: TC_LOGIN_NEG_02

**Title:** Login with non-registered email
**Preconditions:** Email not in DB.
**Steps:**

1. Enter notexist@example.com.
2. Enter any password.
3. Click Login.

**Expected Result:** Login fails. Show message: “User not found” or generic “Incorrect email or password” depending on app rule.
**Test Data:** notexist@example.com / AnyPass123
**Technique Used:** EP (invalid partition)

---

## TC_ID: TC_LOGIN_NEG_03

**Title:** Login with empty email field
**Preconditions:** Login page open.
**Steps:**

1. Leave email empty.
2. Enter valid password.
3. Click Login.

**Expected Result:** Client-side validation: show “Email cannot be empty” (or highlight field). No API call.
**Test Data:** / ValidPass123
**Technique Used:** None (validation)

---

## TC_ID: TC_LOGIN_NEG_04

**Title:** Login with empty password field
**Preconditions:** Login page open.
**Steps:**

1. Enter valid email.
2. Leave password empty.
3. Click Login.

**Expected Result:** Show “Password cannot be empty”. No API call.
**Test Data:** user1@example.com / 
**Technique Used:** None (validation)

---

## TC_ID: TC_LOGIN_NEG_05

**Title:** Login attempts beyond allowed limit → account lockout (rate limiting scenario)
**Preconditions:** Policy: 5 wrong attempts = lockout for 15 minutes. Clean account state.
**Steps:**

1. Enter valid email.
2. Enter wrong password. Repeat 5 times.
3. Try correct password after 5th wrong attempt.

**Expected Result:** After 5th wrong attempt, account locked. Correct password returns “Account locked” (or similar). Verify lockout timestamp in DB or API.
**Test Data:** user1@example.com / WrongPass repeated, then ValidPass123
**Technique Used:** None (security/rate-limit negative)

---

## TC_ID: TC_LOGIN_BVA_01

**Title:** Password length lower boundary (BVA) — minimum allowed (example: min 8)
**Preconditions:** Password policy: min 8, max 16 chars. Account exists.
**Steps:**

1. Enter valid email.
2. Enter password with length = 8 (e.g., Abcde123).
3. Click Login.

**Expected Result:** If password correct, login succeeds. If account password length matched, authentication flows normally. If password is incorrect, only authentication fails (not validation).
**Test Data:** user1@example.com / Abcde123
**Technique Used:** BVA (lower boundary)

---

## TC_ID: TC_LOGIN_BVA_02

**Title:** Password length upper boundary (BVA) — maximum allowed (example: max 16)
**Preconditions:** Password policy: min 8, max 16 chars.
**Steps:**

1. Enter email.
2. Enter password length = 16 (e.g., Abcdefgh12345678).
3. Click Login.

**Expected Result:** Login allowed if password matches stored. If client blocks >16, ensure behaviour is consistent.
**Test Data:** user1@example.com / Abcdefgh12345678
**Technique Used:** BVA (upper boundary)

---

## TC_ID: TC_LOGIN_EP_01

**Title:** EP – valid password partition (pick one representative)
**Preconditions:** Password policy valid length 8–16, contains alpha+digit.
**Steps:**

1. Enter valid email.
2. Enter representative valid password GoodPass12.
3. Click Login.

**Expected Result:** If stored password matches representative, login success. This value stands for whole valid partition.
**Test Data:** user1@example.com / GoodPass12
**Technique Used:** EP

---

## TC_ID: TC_LOGIN_EP_02

**Title:** EP – invalid email format partition (pick one representative)
**Preconditions:** App validates email format client-side.
**Steps:**

1. Enter user1example.com (missing @).
2. Enter any password.
3. Click Login.

**Expected Result:** Client validation blocks and shows “Enter a valid email.” No API call.
**Test Data:** user1example.com / AnyPass
**Technique Used:** EP

---

## TC_ID: TC_LOGIN_DT_01

**Title:** Decision Table: username/password combinations + account status (single table scenario)
**Preconditions:** Accounts: activeUser (active, correct creds), lockedUser (locked), wrongPass available.

**Decision Table (rows = test cases):**

Cond A: Username exists? (Yes/No)
Cond B: Password correct? (Yes/No)
Cond C: Account locked? (Yes/No)

**Rules / Expected outcomes:**

1. A=Yes, B=Yes, C=No → Login success (200).
2. A=Yes, B=No, C=No → Login fail (incorrect credentials).
3. A=Yes, B=No, C=Yes → Login fail (account locked).
4. A=No, B=–, C=– → Login fail (user not found / generic error).

**Test cases (derived):**

* Case 1: activeUser@example.com / ValidPass → success.
* Case 2: activeUser@example.com / WrongPass → incorrect credentials.
* Case 3: lockedUser@example.com / AnyPass → account locked message.
* Case 4: notexist@example.com / AnyPass → user not found / generic error.

**Technique Used:** Decision Table (DT)