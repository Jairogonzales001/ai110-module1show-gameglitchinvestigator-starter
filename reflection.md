# 💭 Reflection: Game Glitch Investigator

Answer each question in 3 to 5 sentences. Be specific and honest about what actually happened while you worked. This is about your process, not trying to sound perfect.

## 1. What was broken when you started?

- What did the game look like the first time you ran it?
- List at least two concrete bugs you noticed at the start  
  (for example: "the hints were backwards").
  1. If the number I enter is lower than the answer hint says Go Lower even if the answer is higher than my guess.
  2. If the number I enter is higher than the answer hint says Go Higher even if the answer is lower than my guess.
  3. Guess should be from 1-100 but it accepts 0 or negative numbers.

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

- Which AI tools did you use on this project (for example: ChatGPT, Gemini, Copilot)? I used claude code during this project to help me understand the bugs and figure out how to fix them. I also used it to explain parts of the code that I did not fully understand.
- Give one example of an AI suggestion that was correct (including what the AI suggested and how you verified the result). 
One suggestion that was correct was updating the check_guess() function so that the higher and lower hints matched the player's guess correctly. I verified this by running the game and testing guesses above and below the secret number.
- Give one example of an AI suggestion that was incorrect or misleading (including what the AI suggested and how you verified the result). 
One suggestion that was misleading was that the game had a state bug causing the secret number to reset every time I clicked Submit. After testing the game myself, I noticed that the secret number was actually staying the same, so that was not one of the bugs I chose to fix.

---

## 3. Debugging and testing your fixes

- How did you decide whether a bug was really fixed?
I decided a bug was fixed by running the game again and repeating the same steps that originally caused the problem. If the game behaved correctly after the change, I considered the bug fixed.
- Describe at least one test you ran (manual or using pytest)  
  and what it showed you about your code.
  One test I ran was entering numbers higher and lower than the secret number to make sure the hints were correct. I also tested invalid inputs such as 0 and negative numbers to verify that they were rejected.
- Did AI help you design or understand any tests? How?
I used pytest to test the check_guess() function. The tests confirmed that the function correctly returned "Win", "Too High", and "Too Low" for different inputs.

---

## 4. What did you learn about Streamlit and state?

- How would you explain Streamlit "reruns" and session state to a friend who has never used Streamlit?
I learned that Streamlit reruns the script every time a user interacts with the page. Because of this, variables can reset unless they are stored in session state.

I would explain session state as a place where Streamlit stores information that needs to be remembered between button clicks and page updates. Without session state, the game would lose important information such as the secret number and score.

---

## 5. Looking ahead: your developer habits

- What is one habit or strategy from this project that you want to reuse in future labs or projects?
One habit I want to continue using is testing my code after every major change instead of waiting until the end. This helped me find problems more quickly.
  - This could be a testing habit, a prompting strategy, or a way you used Git.
- What is one thing you would do differently next time you work with AI on a coding task?
Next time I work with AI on a coding project, I will verify its suggestions more carefully before making changes. Some suggestions were helpful, but others did not match what was actually happening in the program.
- In one or two sentences, describe how this project changed the way you think about AI generated code.
This project showed me that AI can be useful for debugging and learning, but its answers still need to be tested and verified. I learned that I should treat AI as a tool and not assume that every suggestion is correct.
