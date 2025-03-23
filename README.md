## 🎴 **Blackjack Game in Python** 🎮  

This repository contains a **console-based Blackjack game** built using Python. The game simulates the classic card game where the goal is to get as close to **21** as possible without going over. The player competes against the computer (dealer) and can choose to **draw cards** or **hold their score**. Key features include handling **Aces dynamically**, implementing the **dealer’s logic** to draw until 17, and checking for **Blackjack**. The code is organized into **functions** for clarity, using **loops**, **conditional statements**, and **list manipulation** to manage the game flow. Whether you're a beginner learning Python or just looking to play a fun card game, this project is a great example of combining logic and interactivity.

## 🃏 **Overview of the Game**  
The goal of Blackjack is to have cards whose sum is **as close to 21 as possible** without exceeding it.  
- **You (the player)** and the **computer (dealer)** are each dealt **two cards** initially.  
- You can choose to **draw more cards** (hit) or **keep your current hand** (stand).  
- The dealer draws cards until their score is **17 or higher**.  
- The game checks who **wins, loses, or draws** based on the total score.  

---

## 📚 **1. Importing Modules**  
```python
import random
```
- **`import random`**: Imports Python's built-in `random` module to select random cards.   

---

## 🎴 **2. Dealing Cards**  
```python
def deal_card():
    cards = [11, 2, 3, 4, 5, 6, 7, 8, 9, 10, 10, 10, 10]
    return random.choice(cards)
```
### Explanation:  
1. **Function Definition**: `def deal_card()` defines a reusable function.  
2. **Card List**: The deck is represented by a list. Face cards (Jack, Queen, King) are **10** and Ace is **11**.  
3. **Random Choice**: `random.choice(cards)` selects a **random** card from the list.  
4. **Return Statement**: The card is returned to the caller.  

✅ **Concepts Used**: Functions, Lists, Random Module.

---

## 📊 **3. Calculating Scores**  
```python
def calculate_score(cards):
    if sum(cards) == 21 and len(cards) == 2:
        return 0  # Blackjack condition
    score = sum(cards)
    if score > 21 and 11 in cards:
        cards.remove(11)
        cards.append(1)
        score = sum(cards)
    return score
```
### Explanation:  
1. **Blackjack Check**: If there are **2 cards** and their sum is **21**, return `0` to represent **Blackjack**.  
2. **Sum Calculation**: `sum(cards)` adds the values of all cards.  
3. **Ace Adjustment**: If the score is **greater than 21** and **Ace (11)** is present:  
   - **Change** Ace from `11` to `1` to avoid a bust.  
4. **Return Score**: Outputs the adjusted total score.  

✅ **Concepts Used**: If-else statements, List Methods (`remove`, `append`), Sum function.  

---

## 🔍 **4. Comparing Scores**  
```python
def compare(u_score, c_score):
    if u_score == c_score:
        return "Draw 🙃"
    elif c_score == 0:
        return "Lose, opponent has Blackjack 😱"
    elif u_score == 0:
        return "Win with a Blackjack 😎"
    elif u_score > 21:
        return "You went over. You lose 😭"
    elif c_score > 21:
        return "Opponent went over. You win 😁"
    elif u_score > c_score:
        return "You win 😃"
    else:
        return "You lose 😤"
```
### Explanation:  
1. **Comparison Logic**:  
   - If scores are **equal**, it's a draw.  
   - If the **computer** has **Blackjack**, you lose.  
   - If **you** have **Blackjack**, you win.  
   - If **you** exceed **21**, you lose.  
   - If the **computer** exceeds **21**, you win.  
   - Otherwise, the **higher score** wins.  
2. **Return Statements**: Each condition returns a corresponding message.  

✅ **Concepts Used**: Comparison operators, Conditional statements, Function return values.  

---

## 🎮 **5. Main Game Logic**  
```python
def play_game():
    print(logo)
    user_cards = []
    computer_cards = []
    is_game_over = False

    user_cards.append(deal_card())
    user_cards.append(deal_card())
    computer_cards.append(deal_card())
    computer_cards.append(deal_card())
```
### Explanation:  
1. **Game Setup**:  
   - Prints the logo.  
   - Initializes empty **lists** for the player and computer's cards.  
   - Sets `is_game_over` to **False** to track the game state.  
2. **Initial Deal**:  
   - Both the **user** and **computer** get **two random cards** by calling `deal_card()` twice.  

✅ **Concepts Used**: List Initialization, Boolean Flags, Function Calls.

---

## 🔁 **6. User's Turn**  
```python
while not is_game_over:
    user_score = calculate_score(user_cards)
    computer_score = calculate_score(computer_cards)

    print(f"User's card: {user_cards}, Score: {user_score}")
    print(f"Computer's first card: {computer_cards[0]}")

    if user_score == 0 or computer_score == 0 or user_score > 21:
        is_game_over = True
    else:
        second_input = input("Type 'y' to get another card, type 'n' to pass: ")
        if second_input == "y":
            user_cards.append(deal_card())
        else:
            is_game_over = True
```
### Explanation:  
1. **User's Turn Loop**:  
   - **Calculate Scores**: Calls `calculate_score()` for both players.  
   - **Show Cards**: Displays the user’s cards and the **dealer's** first card.  
2. **Stopping Conditions**:  
   - Game ends if the **user** or **computer** has **Blackjack** or the **user** exceeds **21**.  
   - If not, the user decides whether to draw another card (`y`) or pass (`n`).  

✅ **Concepts Used**: While Loop, Input Handling, Condition Checks.

---

## 🤖 **7. Computer’s Turn**  
```python
while computer_score != 0 and computer_score < 17:
    computer_cards.append(deal_card())
    computer_score = calculate_score(computer_cards)
```
### Explanation:  
1. **Dealer Rule**:  
   - The dealer **draws** if their score is **less than 17**.  
   - The loop runs until the dealer's score is at least **17** or if they have **Blackjack**.  

✅ **Concepts Used**: While Loop, Function Call.

---

## 🏆 **8. Display Final Result**  
```python
print(f"Your final hand: {user_cards}, final score: {user_score}")
print(f"Computer's final hand: {computer_cards}, final score: {computer_score}")
print(compare(user_score, computer_score))
```
1. **Display Hands**: Prints both players’ **final cards** and **scores**.  
2. **Determine Winner**: Calls `compare()` to print the **result**.  

---

## 🔁 **9. Game Replay**  
```python
while input("Do you want to play a game of Blackjack? Type 'y' or 'n': ") == "y":
    play_game()
```
1. **Replay Prompt**: Asks the player if they want to play again.  
2. **Loop**: If the player types **"y"**, the game restarts by calling `play_game()`.  

✅ **Concepts Used**: While Loop, Input Handling.

---

## 📌 **Summary of Concepts Used**  
- **Functions** (to organize logic)  
- **Loops** (to repeat game processes)  
- **Conditionals** (to decide outcomes)  
- **Lists** (to store cards)  
- **Random Module** (to shuffle cards)  
- **Input/Output** (to interact with the player)  

Would you like help with improving the game or adding new features? 🚀
