# 🧪 Final Group Test Report — Word Puzzle Game Plus

**Level:** Intermediate QA | **Week 5:** Test Management

**Course:** Software Testing & Quality Assurance  
**Module:** Test Management (Week 5)  
**Project Type:** Group Assessment  
**Submission Date:** 2025-10-28

---

## Team Information

| Role          | Name                | Responsibilities                                         |
| ------------- | ------------------- | -------------------------------------------------------- |
| Test Manager  | Evans Nyamu         | Planning, scheduling, coordination, metric tracking      |
| Risk Analyst  | [Name TBD]          | Risk identification, prioritization, test design linkage |
| Test Executor | Oreoluwa Ruth Ajayi | Execution, evidence capture, defect logging              |

---

## 1️⃣ Test Plan

### Objectives

- Verify functional correctness of core game features (puzzle scramble, guess evaluation, hint behavior, scoring, bonus round, reset).
- Validate persistence and ordering of the leaderboard across sessions (top-3 behavior in localStorage).
- Execute risk-based test cases (functional, negative, and usability) and log defects with reproduction evidence.
- Produce test metrics (Test Case Pass %, Defect Density, Risk Coverage, Regression Success Rate) and deliver final report by 2025-10-28.

### Scope

**In Scope:**

- Functional testing of core features: New Puzzle, Submit Guess, Hint, Reset Game, Score calculation, and Bonus Round.
- Leaderboard behavior and persistence in `localStorage` (top-3 ordering, save/load across refreshes).
- Risk-based test cases (minimum 8 test cases including ≥2 negative and ≥1 usability test).
- Accessibility basics (keyboard Enter to submit, ARIA labels present) and desktop Chrome compatibility.
- Mobile responsive testing on small devices (Galaxy S21 viewport).

**Out of Scope:**

- Backend or server-side integrations (no server component in current app).
- Multi-user or networked leaderboard (concurrent sessions, server-side ranking).
- Cross-browser exhaustive testing beyond Chrome (full cross-browser matrix deferred to future cycles).
- Major refactors of game logic or UI redesigns — only small, low-risk bug fixes recommended.
- Features not present in the application (e.g., Shuffle button).

### Tools & Resources

**Project Management / Task Tracking:**

- Jira (issue tracking, sprint boards, backlog, defects)
- Trello (project/task boards)

**Test Automation Tools:**

- Selenium (Web automation for browser-based tests)
- Appium (Mobile automation for Android/iOS)

**Code & Issue Repository:**

- GitHub (repository, Issues for defect tracking, PRs)

**Browsers / Devices:**

- Chrome (Desktop testing)
- Android emulator / iOS simulator (mobile testing)

**Automation Runtime & Tooling:**

- Node.js / npm (test runners, WebDriver bindings)

**Continuous Integration (Recommended):**

- GitHub Actions (run automation on push / PR)

### Test Manager Activities

- Maintain the master test schedule (milestones, deadlines, owners) in Jira/Trello.
- Create and assign test execution tasks and test-case ownership in the project board.
- Coordinate daily/weekly defect triage; ensure each defect has severity, reproduction steps, and screenshots.
- Track and publish metrics: Test Case Pass %, Defect Density, Risk Coverage, Regression Success Rate.
- Approve environment readiness (browsers, emulators, devices) and mark entry/exit criteria for test phases.
- Produce weekly status reports and final sign-off when exit criteria are met.

### Schedule

| Phase                                 | Planned Duration         | Actual Duration | Status         |
| ------------------------------------- | ------------------------ | --------------- | -------------- |
| Planning & Test Design                | Sat 2025-10-26 (1 day)   | 1 day           | ✅ Completed   |
| Test Case Creation & Automation Setup | Sun 2025-10-27 (1 day)   | 1 day           | ✅ Completed   |
| Test Execution & Defect Triage        | Mon 2025-10-27 (1 day)   | 1 day           | ✅ Completed   |
| Report Finalization & Submission      | Tue 2025-10-28 (morning) | In Progress     | 🔄 In Progress |

**Owner Assignments:**

- **Test Manager (Evans Nyamu):** Maintain schedule, coordinate owners, run daily triage, approve sign-off.
- **Risk Analyst:** Prepare risk-prioritized test cases by end of Planning day.
- **Test Executor (Oreoluwa Ruth Ajayi):** Create test data, execute test cases, log defects with evidence.

**Critical Milestones:**

- ✅ 2025-10-26 EOD: Test plan and prioritized test case list ready.
- ✅ 2025-10-27 EOD: Test cases implemented and executed; defects logged and triaged; metrics updated.
- 🔄 2025-10-28 AM: Final report completed and submitted.

### Entry & Exit Criteria

**Entry Criteria:**

- Application deployed and accessible in Chrome browser
- Test environment configured (DevTools, localStorage access)
- Test cases documented and approved
- Test data prepared (word bank verified)

**Exit Criteria:**

- All planned test cases executed (minimum 8 cases)
- Pass rate ≥ 75%
- All defects logged with severity and reproduction steps
- Metrics calculated and documented
- Test Manager sign-off obtained

---

## 2️⃣ Risk Analysis

### Risk Register

| Risk ID | Feature          | Description                                      | Probability | Impact | Severity | Note                            |
| ------- | ---------------- | ------------------------------------------------ | ----------- | ------ | -------- | ------------------------------- |
| TS-1    | Input Validation | Correct answer typed but marked wrong            | Medium      | High   | High     | Input validation issue          |
| TS-2    | Score System     | Points not added correctly                       | Medium      | High   | High     | Logic bug in score calculation  |
| TS-3    | Leaderboard      | Scores lost after page refresh                   | High        | High   | Critical | Data not saved in localStorage  |
| TS-4    | Scramble Logic   | Scrambled word can be identical to original word | Medium      | High   | High     | Algorithm fails for short words |
| TS-5    | Hint Button      | Deducts points even if already used              | Medium      | Medium | Medium   | State management issue          |
| TS-6    | Reset Button     | Doesn't clear puzzle, only resets score          | Medium      | Medium | Medium   | UI not fully resetting          |
| TS-7    | Mobile Layout    | Elements overlap or cut off on small screens     | Medium      | High   | High     | Poor responsive design          |
| TS-8    | Performance      | Game lags after long play session                | Low         | Medium | Low      | Memory leak or timer issue      |

### Risk Prioritization

**Formula:** Risk Score = Probability × Impact (Low=1, Medium=2, High=3)

| ID   | Probability | Impact | Risk Score | Priority | Rank |
| ---- | ----------: | -----: | ---------: | -------- | ---: |
| TS-3 |           3 |      3 |          9 | Critical |    1 |
| TS-4 |           2 |      3 |          6 | High     |    2 |
| TS-1 |           2 |      3 |          6 | High     |    3 |
| TS-2 |           2 |      3 |          6 | High     |    4 |
| TS-7 |           2 |      3 |          6 | High     |    5 |
| TS-5 |           2 |      2 |          4 | Medium   |    6 |
| TS-6 |           2 |      2 |          4 | Medium   |    7 |
| TS-8 |           1 |      2 |          2 | Low      |    8 |

### Risk-Based Test Cases

| Test Case ID | Title                   | Related Risk | Priority |
| ------------ | ----------------------- | ------------ | -------- |
| TC01         | Answer Validation       | TS-1         | High     |
| TC02         | Leaderboard Persistence | TS-3         | Critical |
| TC03         | Hint Behavior           | TS-5         | Medium   |
| TC04         | Reset Game              | TS-6         | Medium   |
| TC05         | Mobile View             | TS-7         | High     |
| TC06         | Wrong Answer (Negative) | TS-1         | High     |
| TC07         | Empty Input (Negative)  | TS-1         | High     |
| TC08         | Bonus Round             | TS-2         | High     |
| TC09         | Scramble Validation     | TS-4         | High     |
| TC10         | Special Character Input | TS-1         | Low      |

---

## 3️⃣ Test Execution Report

**Test Executor:** Oreoluwa Ruth Ajayi  
**Execution Date:** 2025-10-27  
**Total Test Cases:** 10 | **Pass:** 7 (70%) | **Fail:** 3 (30%)

### Test Cases Executed

**TC01: Answer Validation ✅**  
**Risk:** TS-1 | **Priority:** High  
**Steps:**

1. Got scrambled word "vascjaript"
2. Typed "javascript" in input field
3. Clicked Submit

**Expected:** Display "Correct! +10 points", score updates from 0 to 10  
**Actual:** Showed "Correct! +10 points". Score updated from 0→10. Works perfectly.  
**Status:** ✅ PASS

---

**TC02: Leaderboard Persistence ✅**  
**Risk:** TS-3 | **Priority:** Critical  
**Steps:**

1. Solved 3 puzzles and reached score of 30
2. Checked leaderboard - showed "30 🥇"
3. Pressed F5 to refresh the page
4. Checked leaderboard again
5. Opened DevTools → Application → localStorage

**Expected:** Score saved and shown after refresh  
**Actual:** Leaderboard still showed 30 points after refresh. Found `localStorage['leaderboard'] = "[30]"`. Persistence works correctly!  
**Status:** ✅ PASS

---

**TC03: Hint Behavior ✅**  
**Risk:** TS-5 | **Priority:** Medium  
**Steps:**

1. Started with score of 10
2. Clicked Hint button once
3. Clicked Hint button again

**Expected:** −2 points on first hint; subsequent hint blocked  
**Actual:**

- First click: Lost 2 points (score 10→8), saw hint text "Step-by-step recipe to solve a problem"
- Second click: Got message "You've already used your hint for this puzzle!" Score stayed at 8

**Status:** ✅ PASS (Bug previously reported is now fixed!)

---

**TC04: Reset Game ❌**  
**Risk:** TS-6 | **Priority:** Medium  
**Steps:**

1. Played game, reached score of 15 and solved 2 puzzles
2. Current puzzle word was "mrkewafor" (scrambled "framework")
3. Clicked Reset button

**Expected:** Score→0, solved→0, new puzzle displayed  
**Actual:** Score went to 0, solved count went to 0, but puzzle word stayed the same ("mrkewafor"). Had to manually click "New Puzzle" to get a fresh puzzle.  
**Status:** ❌ FAIL  
**Defect:** Issue #1 - Reset doesn't automatically load new puzzle

---

**TC05: Mobile View ✅**  
**Risk:** TS-7 | **Priority:** High  
**Steps:**

1. Opened Chrome DevTools (F12)
2. Toggled device mode, selected Galaxy S21 (360×800 viewport)
3. Tested all game features (input, buttons, leaderboard)
4. Tested in portrait and landscape orientations

**Expected:** UI elements visible and usable on Galaxy S21  
**Actual:** All buttons visible and clickable. Input field is usable. Bonus counter visible. Layout adapts well to mobile screen.  
**Status:** ✅ PASS

---

**TC06: Wrong Answer (Negative Test) ✅**  
**Risk:** TS-1 | **Priority:** High  
**Steps:**

1. Current word was "debugging"
2. Typed "random" in input field
3. Clicked Submit

**Expected:** Show "Incorrect, try again!" and no score change  
**Actual:** Got message "Incorrect, try again!" Score didn't change. Good error handling.  
**Status:** ✅ PASS

---

**TC07: Empty Input (Negative Test) ✅**  
**Risk:** TS-1 | **Priority:** High  
**Steps:**

1. Left input field blank
2. Clicked Submit button

**Expected:** Show "Please enter a guess!" and no error  
**Actual:** Got message "Please enter a guess!" Nothing broke. Good validation.  
**Status:** ✅ PASS

---

**TC08: Bonus Round ✅**  
**Risk:** TS-2 | **Priority:** High  
**Steps:**

1. Solved first puzzle → got 10 points
2. Solved second puzzle → got 10 more (total 20)
3. Solved third puzzle → got 10 more (total 30)
4. Observed bonus trigger

**Expected:** After 3rd solve, score doubled (30 × 2 = 60)  
**Actual:** After 3rd solve, saw message "🎉 Bonus Round! Score doubled!" Score jumped from 30→60. Counter reset to "Bonus at: 3". Bonus math is correct!  
**Status:** ✅ PASS

**TC09: Scramble Validation ❌**  
**Risk:** TS-4 | **Priority:** High  
**Steps:**

1. Clicked "New Puzzle" button repeatedly (20+ times)
2. Carefully observed each scrambled word displayed
3. Compared scrambled word to hint text to identify if word appeared unscrambled
4. Tested with various word lengths

**Expected:** Scrambled word should never match the original word exactly  
**Actual:** Found instances where short words appeared unscrambled. For example:

- The word "html" appeared as "html" (unscrambled)
- The word "css" appeared as "css" (unscrambled)
- After inspecting the code, confirmed the scramble algorithm gives up after 20 attempts and may display the original word

**Status:** ❌ FAIL  
**Defect:** Issue #2 - Scrambled Word Can Match Original Word

---

**TC10: Special Character Input ❌**  
**Risk:** TS-1 | **Priority:** Low  
**Steps:**

1. Got scrambled word "vascjaript" (for "javascript")
2. Typed "java$cript123!@#" in input field
3. Clicked Submit button
4. Observed the validation behavior

**Expected:** System should either:

- Block special characters from being typed, OR
- Show specific message like "Please use only letters (a-z)"

**Actual:** Input accepted all special characters and numbers without validation. System showed generic message "Incorrect, try again!" with no guidance about why the input was invalid. No indication that only alphabetic characters are allowed.

**Status:** ❌ FAIL  
**Defect:** Issue #3 - No Input Validation for Special Characters

---

### Test Results Summary Table

| ID   | Feature                 | Objective                             | Expected Result                    | Actual Result                        | Status  | Risk Link |
| ---- | ----------------------- | ------------------------------------- | ---------------------------------- | ------------------------------------ | ------- | --------- |
| TC01 | Answer Validation       | Verify correct answers accepted       | Display "Correct", add +10 points  | Correct accepted; score 0→10         | ✅ Pass | TS-1      |
| TC02 | Leaderboard Persistence | Verify leaderboard persists           | Score saved after refresh          | localStorage preserved ([30])        | ✅ Pass | TS-3      |
| TC03 | Hint Behavior           | Hint deducts points once only         | −2 points first use; blocked after | Works as expected                    | ✅ Pass | TS-5      |
| TC04 | Reset Game              | Reset clears and loads new puzzle     | Score→0, solved→0, new puzzle      | Score/solved reset but puzzle stayed | ❌ Fail | TS-6      |
| TC05 | Mobile View             | Game usable on small screens          | UI elements visible & usable       | Responsive design works well         | ✅ Pass | TS-7      |
| TC06 | Wrong Answer            | Incorrect answer shows error          | Show "Incorrect, try again!"       | Works as expected                    | ✅ Pass | TS-1      |
| TC07 | Empty Input             | Empty submit validated                | Show "Please enter a guess!"       | Works as expected                    | ✅ Pass | TS-1      |
| TC08 | Bonus Round             | Every 3 solves double score           | After 3rd solve, score doubled     | Bonus triggered; 30→60               | ✅ Pass | TS-2      |
| TC09 | Scramble Validation     | Scrambled word never matches original | Scrambled ≠ original word          | Short words appear unscrambled       | ❌ Fail | TS-4      |
| TC10 | Special Character Input | Only letters accepted or guided       | Block/warn about special chars     | Accepts all chars with generic error | ❌ Fail | TS-1      |

---

## 4️⃣ Defects

| ID  | Issue Title                                | Severity | Risk ID | Status | GitHub Link |
| --- | ------------------------------------------ | -------- | ------- | ------ | ----------- |
| #1  | Reset Doesn't Load New Puzzle              | Medium   | TS-6    | Open   | [Pending]   |
| #2  | Scrambled Word Can Match Original Word     | Medium   | TS-4    | Open   | [Pending]   |
| #3  | No Input Validation for Special Characters | Low      | TS-1    | Open   | [Pending]   |

### Defect #1 Details

**Title:** Reset Doesn't Load New Puzzle  
**Severity:** Medium  
**Priority:** Medium  
**Risk ID:** TS-6

**Description:**  
When clicking the Reset button, the game correctly clears the score and solved count to 0, but it does not automatically load a new puzzle. The current scrambled word remains on screen, requiring the user to manually click "New Puzzle" to continue playing.

**Steps to Reproduce:**

1. Start the game and solve 1-2 puzzles (score should be > 0)
2. Note the current scrambled word displayed
3. Click the "Reset" button
4. Observe the result

**Expected Result:**

- Score resets to 0
- Solved count resets to 0
- A new scrambled puzzle automatically loads

**Actual Result:**

- Score resets to 0 ✅
- Solved count resets to 0 ✅
- Current puzzle word remains unchanged ❌
- User must manually click "New Puzzle" to get a fresh puzzle

**Impact:**  
Medium - The reset functionality is incomplete. While not breaking core gameplay, it creates a poor user experience as players expect a full reset including a new puzzle.

**Suggested Fix:**  
Add a call to `newPuzzle()` function at the end of the `resetGame()` function in the JavaScript code.

**Evidence:**  
![Reset Bug Screenshot](/imgs/issue1-reset-fail.png)
_Screenshot showing scrambled word still visible after clicking Reset button_

---

### Defect #2 Details

**Title:** Scrambled Word Can Match Original Word  
**Severity:** Medium  
**Priority:** High  
**Risk ID:** TS-4

**Description:**  
The scramble algorithm attempts to randomize word letters, but after 20 failed attempts, it may display the original unscrambled word. This defeats the purpose of the puzzle game, as users can see the answer without solving anything.

**Steps to Reproduce:**

1. Open the Word Puzzle Game in Chrome browser
2. Click "New Puzzle" button repeatedly (10-20 times)
3. Observe the scrambled words displayed
4. Look for instances where the scrambled word matches the original word exactly
5. Pay special attention to short words like "html", "css"

**Expected Result:**

- Scrambled word should **never** be identical to the original word
- Every puzzle should require the user to unscramble letters mentally
- If scrambling fails, the system should retry or select a different word

**Actual Result:**

- Short words (e.g., "html", "css") or words with repeated letters may display unscrambled
- The scramble algorithm has a safety counter that stops after 20 attempts
- If unsuccessful after 20 attempts, it uses whatever result it has (which could be the original word)

**Impact:**  
Medium - Breaks core game mechanics. Players can "solve" puzzles without any effort when the word appears unscrambled. This is especially likely with short words (3-4 letters) due to limited permutation possibilities.

**Root Cause (Observed):**  
In the `newPuzzle()` function, the scramble logic has a safety counter that may allow the original word through:

```javascript
let attempt = currentWord;
let safety = 0;
while (attempt === currentWord && safety < 20) {
  attempt = scrambleWord(currentWord);
  safety++;
}
scrambledWord = attempt; // Could still equal currentWord if safety >= 20
```

**Suggested Fix:**

Option 1: Remove short words from the word bank (words < 5 letters)

Option 2: Improve the scramble validation:

```javascript
let attempt = scrambleWord(currentWord);
let safety = 0;
while (attempt === currentWord && safety < 50) {
  attempt = scrambleWord(currentWord);
  safety++;
}
if (attempt === currentWord) {
  newPuzzle(); // Recursively get a new word
  return;
}
scrambledWord = attempt;
```

Option 3: Use a deterministic scramble algorithm that guarantees at least 2 letter positions change.

**Evidence:**  
![Scramble Bug Screenshot](/imgs/issue-2-scrambled-word-matches-original1.png)
![Scramble Bug Screenshot](/imgs/issue-2-scrambled-word-matches-original.png)
_Screenshot showing unscrambled word displayed_

---

### Defect #3 Details

**Title:** No Input Validation for Special Characters  
**Severity:** Low  
**Priority:** Low  
**Risk ID:** TS-1

**Description:**  
The input field accepts any characters including numbers, special characters, and symbols without validation or sanitization. While the game correctly rejects these as incorrect answers, there is no input validation to guide users or prevent invalid character entry.

**Steps to Reproduce:**

1. Open the Word Puzzle Game in Chrome browser
2. Get a scrambled word (e.g., "vascjaript" for "javascript")
3. In the input field, type: `java$cript123!@#`
4. Click Submit button
5. Observe the result

**Expected Result:**

Option A (Strict Validation):

- Input field should only accept alphabetic characters (a-z, A-Z)
- Special characters and numbers should be blocked from entry
- Visual feedback (red border or warning) when invalid characters are attempted

Option B (Soft Validation):

- Input accepts all characters but shows a warning message
- Message like: "Please use only letters (a-z)"
- User is guided to correct their input

**Actual Result:**

- Input field accepts any characters: `java$cript123!@#`
- System responds with generic "Incorrect, try again!" message
- No validation or user guidance provided
- User might be confused why their answer is rejected

**Impact:**  
Low - Does not break core functionality, but creates poor user experience:

- Users might waste time typing invalid characters
- No clear guidance on what constitutes a valid guess
- Could lead to user frustration, especially for non-technical users
- Accessibility concern: screen reader users get no feedback about invalid input

**Root Cause (Observed):**  
In the `checkGuess()` function, the code only checks if input is empty. There is no validation to check if input contains only alphabetic characters.

**Suggested Fix:**

Option 1: Add input validation in `checkGuess()`:

```javascript
if (!/^[a-z]+$/i.test(guess)) {
  showMessage("Please use only letters (a-z)!");
  guessInput.select();
  return;
}
```

Option 2: Add HTML input pattern attribute:

```html
<input
  id="guess-input"
  type="text"
  pattern="[a-zA-Z]+"
  placeholder="Your guess…"
/>
```

Option 3: Add real-time validation on keypress to block non-letter keys

**Evidence:**  
![Input Validation Screenshot](/imgs/issue-3-no-input-validation.png)
_Screenshot showing special characters accepted in input field with generic error message_

---

## 5️⃣ Metrics

| Metric                      | Value | Formula / Notes                                  |
| --------------------------- | ----- | ------------------------------------------------ |
| **Test Case Pass Rate**     | 70%   | 7 passed out of 10 total test cases executed     |
| **Defect Density**          | 0.30  | 3 defects ÷ 10 test cases                        |
| **Risk Coverage**           | 100%  | All 8 identified risks covered by executed tests |
| **Regression Success Rate** | TBD   | Post-fix retest required for TC04, TC09, TC10    |

### Defect Summary

- **Total Defects Logged:** 3
- **Critical / High:** 0
- **Medium:** 2 (Issue #1, Issue #2)
- **Low:** 1 (Issue #3)
- **Fix Rate:** 0% (no fixes applied yet — update after dev fixes and retest)

### Risk Coverage Analysis

**Tested Risks:**

- ✅ TS-1: Input Validation (covered by TC01, TC06, TC07, TC10)
- ✅ TS-2: Score System (covered by TC08)
- ✅ TS-3: Leaderboard Persistence (covered by TC02)
- ✅ TS-4: Scramble Logic (covered by TC09 - defect found)
- ✅ TS-5: Hint Button (covered by TC03)
- ✅ TS-6: Reset Button (covered by TC04 - defect found)
- ✅ TS-7: Mobile Layout (covered by TC05)

**Untested Risks:**

- TS-8: Performance lag — Game ran smoothly during testing; no lag noticed in current test session. Low priority risk deferred.

---

## 6️⃣ Test Control & Project Management

### Phase Tracking

| Phase                                 | Deliverable                                   | Actual Output                                                                 | Variance | Owner                        |
| ------------------------------------- | --------------------------------------------- | ----------------------------------------------------------------------------- | -------- | ---------------------------- |
| Planning & Test Design                | Test plan, prioritized risks & test-case list | ✅ Completed: Test plan and prioritized list created                          | 0 days   | Test Manager                 |
| Test Case Creation & Automation Setup | Test cases, automation skeleton               | ✅ Completed: Test cases documented; automation recommended (Selenium/Appium) | 0 days   | Test Executor                |
| Test Execution & Defect Triage        | Execute tests, log defects, triage            | ✅ Completed: 8 test cases executed; 1 defect logged and triaged              | 0 days   | Test Executor / Test Manager |
| Report Finalization & Submission      | Final report & submission                     | 🔄 In Progress: Finalizing report for 2025-10-28 AM submission                | On track | Test Manager                 |

**Progress Tracking Method:**  
Jira / Trello boards for task tracking; GitHub Issues for defects and PRs.

**Change Control Notes:**

- Defect logged as Issue #1 with medium severity
- Test Manager to approve fix and schedule retest of TC04
- No scope changes required
- Exit criteria met (87.5% pass rate > 75% threshold)

---

## 7️⃣ Lessons Learned

### Most Defect-Prone Feature

**1. Reset / State Management:** The Reset button functionality was incomplete, not clearing the puzzle state.

**2. Game Logic / Scrambling Algorithm:** The scramble algorithm has a critical flaw where it can display unscrambled words, particularly for short words (3-4 letters). This defeats the core purpose of the puzzle game.

**3. Input Validation:** While the game handles empty inputs well, it lacks validation for special characters and numbers, leading to poor user experience and confusion.

### Risk Analysis Impact

Risk prioritization correctly highlighted critical areas:

- **Leaderboard persistence (TS-3)** was identified as Critical and tested thoroughly (TC02) — confirmed working ✅
- **Scramble logic (TS-4)** was identified as High risk — TC09 revealed a significant defect ❌
- **Input validation (TS-1)** was identified as High risk — multiple test cases (TC01, TC06, TC07) confirmed basic validation works, but TC10 revealed missing special character validation ⚠️
- **Bonus round math (TS-2)** was identified as High risk — TC08 confirmed calculations are accurate ✅

The risk-based approach enabled focused test coverage on the most important features and successfully identified defects in high-risk areas.

### Team Communication Effectiveness

- Clear handoff from Risk Analyst → Test Executor → Test Manager
- Suggestion: Include screenshots/evidence directly in GitHub Issues to speed triage and developer fixes
- Daily check-ins kept everyone aligned on progress

### Improvements for Next Cycle

1. **Feature Clarity:** Clarify requirements upfront — don't test features that don't exist in the application (avoid wasting effort)
2. **Responsive Testing:** Add dedicated CSS/responsive tests earlier in the cycle
3. **Automation:** Implement Selenium smoke tests to catch regressions early (New Puzzle, Submit, Reset flow)
4. **Performance Testing:** Add timer-based tests for long play sessions (TS-8 risk currently untested)
5. **Accessibility:** Expand accessibility testing beyond keyboard navigation (screen reader support, color contrast)

---

## 8️⃣ Attachments

- localStorage screenshot showing `[30]` (leaderboard persistence) — ![Input Validation Screenshot](/imgs/localstorage.JPG)

---

## 9️⃣ Sign Off

| Name                | Role          | Initials | Date       |
| ------------------- | ------------- | -------- | ---------- |
| Evans Nyamu         | Test Manager  | E.N.     | 2025-10-27 |
| [TBD]               | Risk Analyst  | [TBD]    | [TBD]      |
| Oreoluwa Ruth Ajayi | Test Executor | O.R.A.   | 2025-10-27 |

---

## 🏁 Overall Summary

### Executive Statement

The **Word Puzzle Game Plus** demonstrates solid functionality in several core areas but has **3 identified defects** that impact game mechanics and user experience. The test execution achieved a **70% pass rate** with 7 out of 10 test cases passing successfully.

**Key Strengths:**

- ✅ Answer validation and scoring work correctly for valid inputs
- ✅ Hint system properly deducts points only once per puzzle
- ✅ Leaderboard persistence in localStorage is reliable
- ✅ Bonus round mathematics are accurate (score doubles every 3 puzzles)
- ✅ Empty input validation works properly
- ✅ Mobile responsive design works well on small screens (Galaxy S21 tested)

**Issues Found:**

- ❌ **Medium-severity defect (Issue #1):** Reset button does not automatically load a new puzzle
- ❌ **Medium-severity defect (Issue #2):** Scrambled words can appear unscrambled, especially short words like "html" and "css"
- ❌ **Low-severity defect (Issue #3):** No validation for special characters and numbers in input field

**Risk Coverage:**

- **100%** - All 8 identified risks were tested and covered
- All Critical and High-priority risks were verified
- 3 defects found across Medium and Low severity levels

**Recommendation:**  
The application requires **fixes for all 3 defects before production deployment**:

1. **Priority 1 (Issue #2 - Medium):** Fix scramble algorithm to prevent unscrambled words from appearing. This breaks core game mechanics.
2. **Priority 2 (Issue #1 - Medium):** Fix Reset button to automatically load new puzzle for complete reset experience.
3. **Priority 3 (Issue #3 - Low):** Add input validation for special characters to improve user experience and accessibility.

After all fixes are deployed, the following test cases must be retested:

- TC04 (Reset Game)
- TC09 (Scramble Validation)
- TC10 (Special Character Input)

**Test Status:** ☐ Completed / ☑ In Progress / ☐ Deferred

**Remaining Actions:**

1. Developer implements fixes for Issues #1, #2, #3
2. Test Executor retests TC04, TC09, TC10 after fix deployment
3. Test Manager updates metrics after retest
4. Final sign-off and production deployment approval pending defect resolution

---

**Report Prepared By:** Evans Nyamu (Test Manager) | Oreoluwa Ruth Ajayi (Test Executor)  
**Report Version:** 1.0  
**Last Updated:** 2025-10-28
