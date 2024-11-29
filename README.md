# Basic-Game-Tic-Tac
# **Tic Tac Game**

## **Overview**
The **Tic Tac** game is a simple two-player implementation of the classic **Tic-Tac-Toe** using Python's `tkinter` library. The game is visually appealing and user-friendly, featuring an interactive 3x3 grid, status updates for players, and a "Play Again" button for repeated gameplay.

---

## **Objective**
To create a visually engaging and interactive Tic-Tac-Toe game where two players (X and O) can:
- Take turns marking their symbols.
- Determine the winner when a player aligns their symbols horizontally, vertically, or diagonally.
- Replay the game after a win or draw.

---

## **Features**
1. **Two-Player Gameplay**:
   - Players alternate between "X" and "O".
   - Status label updates to show whose turn it is.

2. **Win Detection**:
   - Recognizes wins in rows, columns, and diagonals.
   - Displays the winner's name ("X won!" or "O won!") or declares a draw.

3. **Replay Option**:
   - After a game ends (win or draw), players can click "Play Again" to reset the grid and start a new match.

4. **Disable Game After Win**:
   - Once a winner is determined, further moves are disabled to maintain game integrity.

---

## **Technology Stack**
- **Programming Language**: Python
- **GUI Library**: `tkinter`

---

## **Game Design**

### **1. Layout**
- **Main Window**:
  - Title: `"Tic Tac"`
  - Resizable: `False` for consistent layout across devices.
- **Header**: A label displaying `"Tic Tac"` with a large font.
- **Status Label**: Displays the current player's turn or the result of the game.
- **Grid**:
  - A 3x3 grid of buttons representing the Tic-Tac-Toe board.
  - Buttons are dynamically styled and reset between games.

### **2. Classes**
- **`XOPoint`**:
  - Represents each cell in the grid.
  - Tracks its position (`x, y`) and value (`X`, `O`, or empty).
  - Provides methods for setting/resetting the cell.

- **`WinningPossibility`**:
  - Defines potential winning combinations (rows, columns, and diagonals).
  - Checks if a player satisfies a specific winning condition.

---

## **Code Explanation**

### **1. Game Initialization**
- **Root Window**:
  - Create the main application window with a fixed size and title.
  - Add a status label to indicate turns or game results.
  ```python
  root = tk.Tk()
  root.resizable(False, False)
  root.title("Tic Tac")
  ```

### **2. Gameplay Functions**
- **Set Cell**:
  - Marks a cell with the current player's symbol (`X` or `O`) and updates the status label.
  - Switches the turn to the other player and checks for a win condition.
  ```python
  def set(self):
      global current_chr
      if not self.value:
          self.button.configure(text=current_chr, bg='snow', fg='black')
          self.value = current_chr
          if current_chr == "X":
              X_points.append(self)
              current_chr = "O"
              status_label.configure(text="O's turn")
          elif current_chr == "O":
              O_points.append(self)
              current_chr = "X"
              status_label.configure(text="X's turn")
      check_win()
  ```

- **Check Win**:
  - Iterates through all predefined winning possibilities to check if a player has won.
  - Disables the game board and displays the winner if a condition is met.
  ```python
  def check_win():
      for possibility in winning_possibilities:
          if possibility.check('X'):
              status_label.configure(text="X won!")
              disable_game()
              return
          elif possibility.check('O'):
              status_label.configure(text="O won!")
              disable_game()
              return
      if len(X_points) + len(O_points) == 9:
          status_label.configure(text="Draw!")
          disable_game()
  ```

- **Play Again**:
  - Resets the grid, clears player data, and restores the default game state.
  ```python
  def play_again():
      global current_chr
      current_chr = 'X'
      for point in XO_points:
          point.button.configure(state=tk.NORMAL)
          point.reset()
      status_label.configure(text="X's turn")
      play_again_button.pack_forget()
  ```

---

### **3. Game Components**
- **Grid Cells**:
  - Implemented using the `XOPoint` class.
  - Dynamically created for a 3x3 grid.
- **Winning Combinations**:
  - Predefined rows, columns, and diagonals using the `WinningPossibility` class.
  ```python
  winning_possibilities = [
      WinningPossibility(1, 1, 1, 2, 1, 3),
      WinningPossibility(2, 1, 2, 2, 2, 3),
      WinningPossibility(3, 1, 3, 2, 3, 3),
      WinningPossibility(1, 1, 2, 1, 3, 1),
      WinningPossibility(1, 2, 2, 2, 3, 2),
      WinningPossibility(1, 3, 2, 3, 3, 3),
      WinningPossibility(1, 1, 2, 2, 3, 3),
      WinningPossibility(3, 1, 2, 2, 1, 3)
  ]
  ```

---

## **How to Use**
1. **Start the Game**:
   - Run the script to launch the application.
   - The status label will display `"X's turn"`.
2. **Gameplay**:
   - Players take turns clicking on empty cells.
   - The grid updates with the current player's symbol (`X` or `O`).
3. **Game Over**:
   - The game ends when:
     - A player wins (row, column, or diagonal alignment).
     - All cells are filled with no winner (draw).
   - The status label displays the result.
4. **Replay**:
   - Click "Play Again" to reset the game board.

---

## **Complete Code**
```python
<Insert Code Here>
```

---

## **Conclusion**
The **Tic Tac** game provides a foundational understanding of GUI development in Python. With dynamic components, win-check logic, and replay functionality, it serves as a stepping stone for more complex applications.
