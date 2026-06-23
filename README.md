# 🎮 Game Glitch Investigator: The Impossible Guesser

## 🚨 The Situation

This project is a simple number guessing game built with Streamlit. The player selects a difficulty level and tries to guess the secret number before running out of attempts. The game gives hints after each guess and keeps track of the score.

## 🛠️ Setup

1. Install dependencies: `pip install -r requirements.txt`
2. Run the app: `python -m streamlit run app.py`

## 🕵️‍♂️ Bugs Found and Fixed

1. The higher/lower hints were backwards. When the guess was too low, the game said to go lower. When the guess was too high, the game said to go higher.
2. The game accepted guesses outside the valid range, such as `0` and negative numbers.
3. The main game logic was inside `app.py`, so I moved the reusable logic into `logic_utils.py` to make it easier to test.

## 📸 Demo Walkthrough

1. I started the app by running `python -m streamlit run app.py`.
2. I selected the difficulty level from the sidebar.
3. I entered a guess lower than the secret number, and the game correctly told me to go higher.
4. I entered a guess higher than the secret number, and the game correctly told me to go lower.
5. I tested invalid guesses like `0` and `-5`, and the game showed an error message instead of accepting them.
6. I guessed the correct number, and the game showed the winning message and final score.

## 🧪 Test Results

```text
tests/test_game_logic.py ...                                             [100%]
============================== 3 passed in 0.01s ===============================