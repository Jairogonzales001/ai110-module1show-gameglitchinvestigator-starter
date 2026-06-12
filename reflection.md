# 💭 Reflection: Game Glitch Investigator

Answer each question in 3 to 5 sentences. Be specific and honest about what actually happened while you worked. This is about your process, not trying to sound perfect.

## 1. What was broken when you started?

- What did the game look like the first time you ran it?
- List at least two concrete bugs you noticed at the start  
  (for example: "the hints were backwards").
  1. If the number I enter is lower than the answer hint says Go Lower even if the answer is higher than my guess.
  2. If the number I enter is higher than the answer hint says Go Higher even if the answer is lower than my guess.
  3. New Game button does not work. 
  4. Normal difficulty has more attempts than easy
  5. Guess should be from 1-100 but it accepts 0 or negative numbers.

**Bug Reproduction Log**

Document at least 3 bugs you found. Add rows as needed.

| Input Used | Expected Behavior | Actual Behavior | Console Error / Output |
|------------|-------------------|-----------------|------------------------|
| Secret = 50 (from Developer Debug Info), enter `80` | Guess is too high, so hint should say "📉 Go LOWER!" | Hint says "📈 Go HIGHER!" — the hints are reversed | No error thrown; the int-vs-string comparison raises a `TypeError` that is silently caught in `check_guess`, so the wrong hint just shows |
| Secret = 50 (from Developer Debug Info), enter `30` | Guess is too low, so hint should say "📈 Go HIGHER!" | Hint says "📉 Go LOWER!" — the hints are reversed | No error thrown |
| Win or lose a round, then click **New Game 🔁** | Game fully resets (attempts, score, history, status) and lets me play again | Page still shows "You already won / Game over. Start a new game to try again." and stops — `status` and `history` are never reset, so the game stays stuck | No error thrown |
| Select **Easy**, note attempts; then select **Normal** | Easy should give the most attempts; Normal should give fewer | Easy shows 6 attempts but Normal shows 8 — Normal gives *more* attempts than Easy | No error thrown |
| Enter `0` (or `-5`) as a guess and click Submit | Rejected with a message like "Enter a number between 1 and 100." | Accepted as a valid guess and scored — `parse_guess` only checks that it's an integer, never the 1–100 range | No error thrown |

---

## 2. How did you use AI as a teammate?

- Which AI tools did you use on this project (for example: ChatGPT, Gemini, Copilot)?
- Give one example of an AI suggestion that was correct (including what the AI suggested and how you verified the result).
- Give one example of an AI suggestion that was incorrect or misleading (including what the AI suggested and how you verified the result).

---

## 3. Debugging and testing your fixes

- How did you decide whether a bug was really fixed?
- Describe at least one test you ran (manual or using pytest)  
  and what it showed you about your code.
- Did AI help you design or understand any tests? How?

---

## 4. What did you learn about Streamlit and state?

- How would you explain Streamlit "reruns" and session state to a friend who has never used Streamlit?

---

## 5. Looking ahead: your developer habits

- What is one habit or strategy from this project that you want to reuse in future labs or projects?
  - This could be a testing habit, a prompting strategy, or a way you used Git.
- What is one thing you would do differently next time you work with AI on a coding task?
- In one or two sentences, describe how this project changed the way you think about AI generated code.
