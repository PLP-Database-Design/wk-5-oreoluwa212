# Issue #1: Reset Button Doesn't Load New Puzzle

**Severity:** Medium  
**Risk Impact ID:** TS-6  
**Reported by:** Oreoluwa Ruth Ajayi (Test Executor)  
**Status:** Open

## Summary

When the user clicks the Reset button, the score and solved count reset to 0, but the scrambled word display remains unchanged. The UI shows "Game reset!" message but the puzzle does not refresh, forcing users to manually click "New Puzzle" to continue playing.

## Steps to Reproduce

1. Open the Word Puzzle Game in Chrome browser
2. Play the game and solve 1-2 puzzles (score should be greater than 0)
3. Note the current scrambled word displayed (e.g., "mrkewafor")
4. Click the "Reset" button at the bottom of the game controls
5. Observe the result

## Expected Result

- Score resets to 0
- Solved count resets to 0
- Message displays "Game reset!"
- **A new scrambled puzzle automatically loads and displays**

## Actual Result

- Score resets to 0 ✓
- Solved count resets to 0 ✓
- Message displays "Game reset!" ✓
- **The scrambled word display remains empty because the pop-up persists for too long** ❌
- User must manually click "New Puzzle" button to get a fresh puzzle immediately or wait

## Impact

**Medium** - Creates confusing user experience. Users expect a complete reset including a new puzzle, but the "Game reset!" display remains visible. This breaks the mental model of what "reset" means and requires an extra manual step.

## Root Cause (Observed)

In the `resetGame()` function (line ~235), the code clears the state variables and updates the UI, but does not call `newPuzzle()` to load a fresh puzzle. The scrambled word element is cleared (`scrambledWordEl.textContent = ""`) but no new puzzle is generated.

## Suggested Fix

Add a call to `newPuzzle()` at the end of the `resetGame()` function:

```javascript
function resetGame() {
  score = 0;
  puzzlesSolved = 0;
  hintUsed = false;

  scoreEl.textContent = score;
  solvedEl.textContent = puzzlesSolved;
  updateNextBonusIndicator();

  messageEl.textContent = "Game reset!";
  messageEl.className = "success";
  scrambledWordEl.textContent = "";
  hintEl.textContent = "";
  guessInput.value = "";
  guessInput.focus();

  // ADD THIS LINE:
  newPuzzle(); // Load a fresh puzzle after reset
}
```

## Test Case Reference

**TC04: Reset Game** (Failed)

## Screenshots

![Reset Bug Screenshot](/imgs/issue1-reset-fail.png)
_Screenshot showing scrambled word still visible after clicking Reset button_

## Labels

`bug` `medium-priority` `ux` `state-management`
