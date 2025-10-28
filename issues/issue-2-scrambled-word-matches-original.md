# Issue #2: Scrambled Word Can Match Original Word

**Severity:** Medium  
**Risk Impact ID:** TS-4 (Game Logic)  
**Reported by:** Oreoluwa Ruth Ajayi (Test Executor)  
**Status:** Open

## Summary

The scramble algorithm attempts to randomize word letters, but after 20 failed attempts, it may display the original unscrambled word. This defeats the purpose of the puzzle game, as users can see the answer without solving anything.

## Steps to Reproduce

1. Open the Word Puzzle Game in Chrome browser
2. Click "New Puzzle" button repeatedly (10-20 times)
3. Observe the scrambled words displayed
4. Look for instances where the scrambled word matches the original word exactly
5. Pay special attention to short words like "html", "css"

## Expected Result

- Scrambled word should **never** be identical to the original word
- Every puzzle should require the user to unscramble letters mentally
- If scrambling fails, the system should retry or select a different word

## Actual Result

- Short words (e.g., "html", "css") or words with repeated letters may display unscrambled
- The scramble algorithm has a safety counter that stops after 20 attempts
- If unsuccessful after 20 attempts, it uses whatever result it has (which could be the original word)

## Impact

**Medium** - Breaks core game mechanics. Players can "solve" puzzles without any effort when the word appears unscrambled. This is especially likely with short words (3-4 letters) due to limited permutation possibilities.

## Root Cause (Observed)

In the `newPuzzle()` function (line ~170-178), the scramble logic has a safety counter:

```javascript
let attempt = currentWord;
let safety = 0;
while (attempt === currentWord && safety < 20) {
  attempt = scrambleWord(currentWord);
  safety++;
}
scrambledWord = attempt; // Could still equal currentWord if safety >= 20
```

If after 20 attempts the scrambled word still matches the original, it proceeds anyway.

## Suggested Fix

**Option 1:** Remove short words from the word bank (words < 5 letters)

**Option 2:** Improve the scramble validation:

```javascript
let attempt = scrambleWord(currentWord);
let safety = 0;
while (attempt === currentWord && safety < 50) {
  attempt = scrambleWord(currentWord);
  safety++;
}
// If still equal after 50 attempts, pick a different word entirely
if (attempt === currentWord) {
  newPuzzle(); // Recursively get a new word
  return;
}
scrambledWord = attempt;
```

**Option 3:** Use a deterministic scramble algorithm that guarantees at least 2 letter positions change.

## Test Case Reference

**TC09: Scramble Validation** (New test case - should be added)

## Screenshots

![Scramble Bug Screenshot](/imgs/issue-2-scrambled-word-matches-original1.png)
![Scramble Bug Screenshot](/imgs/issue-2-scrambled-word-matches-original.png)
_Screenshot showing unscrambled word displayed_

## Labels

`bug` `medium-priority` `game-logic` `algorithm`
