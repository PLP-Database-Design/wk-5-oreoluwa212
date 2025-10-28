# Issue #3: No Input Validation for Special Characters

**Severity:** Low  
**Risk Impact ID:** TS-1 (Input Validation)  
**Reported by:** Oreoluwa Ruth Ajayi (Test Executor)  
**Status:** Open

## Summary
The input field accepts any characters including numbers, special characters, and symbols without validation or sanitization. While the game correctly rejects these as incorrect answers, there is no input validation to guide users or prevent invalid character entry.

## Steps to Reproduce
1. Open the Word Puzzle Game in Chrome browser
2. Get a scrambled word (e.g., "vascjaript" for "javascript")
3. In the input field, type: `java$cript123!@#`
4. Click Submit button
5. Observe the result

## Expected Result
**Option A (Strict Validation):**
- Input field should only accept alphabetic characters (a-z, A-Z)
- Special characters and numbers should be blocked from entry
- Visual feedback (red border or warning) when invalid characters are attempted

**Option B (Soft Validation):**
- Input accepts all characters but shows a warning message
- Message like: "Please use only letters (a-z)"
- User is guided to correct their input

## Actual Result
- Input field accepts any characters: `java$cript123!@#`
- System responds with generic "Incorrect, try again!" message
- No validation or user guidance provided
- User might be confused why their answer is rejected

## Impact
**Low** - Does not break core functionality, but creates poor user experience:
- Users might waste time typing invalid characters
- No clear guidance on what constitutes a valid guess
- Could lead to user frustration, especially for non-technical users
- Accessibility concern: screen reader users get no feedback about invalid input

## Root Cause (Observed)
In the `checkGuess()` function (line ~191), the code only checks if input is empty:

```javascript
function checkGuess(){
  const guess = guessInput.value.trim().toLowerCase();
  if(!guess){
    showMessage("Please enter a guess!");
    return;
  }
  if(guess === currentWord){
    // Correct answer logic...
  } else {
    showMessage("Incorrect, try again!");
    guessInput.select();
  }
}
```

There is no validation to check if `guess` contains only alphabetic characters.

## Suggested Fix

**Option 1:** Add input validation in `checkGuess()`:
```javascript
function checkGuess(){
  const guess = guessInput.value.trim().toLowerCase();
  if(!guess){
    showMessage("Please enter a guess!");
    return;
  }
  
  // Add validation for alphabetic characters only
  if(!/^[a-z]+$/i.test(guess)){
    showMessage("Please use only letters (a-z)!");
    guessInput.select();
    return;
  }
  
  if(guess === currentWord){
    // Correct answer logic...
  } else {
    showMessage("Incorrect, try again!");
    guessInput.select();
  }
}
```

**Option 2:** Add HTML input pattern attribute:
```html
<input id="guess-input" 
       type="text" 
       pattern="[a-zA-Z]+" 
       placeholder="Your guess…" 
       autocomplete="off" />
```

**Option 3:** Add real-time validation on keypress:
```javascript
guessInput.addEventListener('keypress', e => {
  if(!/[a-zA-Z]/.test(e.key)){
    e.preventDefault(); // Block non-letter keys
  }
  if(e.key === 'Enter') checkGuess();
});
```

## Test Case Reference
**TC10: Special Character Input Validation**

## Screenshots
![Input Validation Screenshot](/imgs/issue-3-no-input-validation.png)
*Screenshot showing special characters accepted in input field with generic error message*

## Labels
`enhancement` `low-priority` `input-validation` `ux` `accessibility`