# Tic-Tac-Toe Game-Playing AI (Minimax)

An adversarial search agent that plays Tic-Tac-Toe against a human on a 3x3 grid. On its turn, the AI uses the **Minimax** algorithm (optionally with **Alpha-Beta pruning**) to search every possible future move, assuming the opponent also plays optimally, and picks the move with the best guaranteed outcome. Because the Tic-Tac-Toe game tree is small enough to search completely, the AI plays perfectly and can never lose.

This project solves the general two-player, turn-based, zero-sum game-playing problem, a core building block for board-game agents and decision-making under competition.

> **Course:** 02AML204 – Introduction to Artificial Intelligence
> **Assignment:** SLE-3 – Architectural Design (Full C4 Model)

## Features

- Human vs. AI play in the terminal
- Move validation (cells 1–9, must be empty)
- Win and draw detection after every move
- Perfect-play AI using Minimax (optional Alpha-Beta pruning)
- Game rules kept separate from AI logic, so the AI can be swapped out
- Self-contained: no network, API, or third-party dependencies

## Getting Started

### Requirements

- Python 3.8 or newer

### Run

```bash
python tictactoe.py
```

> Replace `tictactoe.py` with the actual name of your script.

### How to play

1. The board cells are numbered 1–9, left to right, top to bottom:

   ```
    1 | 2 | 3
   ---+---+---
    4 | 5 | 6
   ---+---+---
    7 | 8 | 9
   ```

2. On your turn, enter the number of an empty cell.
3. The AI replies with its move and the updated board is shown.
4. The game ends when someone completes a line (player wins or AI wins) or the board fills up (draw).

## How the AI Works

Minimax scores each finished game from the AI's point of view:

| Outcome        | Score |
|----------------|:-----:|
| AI wins        | +1    |
| Draw           | 0     |
| Player wins    | −1    |

The AI (maximizer) picks the move with the highest score, assuming the player (minimizer) always picks the lowest. The search is a recursive place → recurse → undo loop over the list of empty cells.

## Architecture (C4 Model)

The full C4 diagrams (Context, Container, Component) are in the SLE-3 report. A summary follows.

### Level 1 – Context

The **User** picks an empty cell. The **Tic-Tac-Toe AI system** validates the move, replies with its own, and returns the updated board and, at the end, the result. There are no external systems.

### Level 2 – Containers

| Container        | Responsibility                                                                 |
|------------------|--------------------------------------------------------------------------------|
| **Input module** | Reads the chosen cell (1–9) and checks it is valid and still empty             |
| **Game engine**  | Controls turn order, applies moves, checks for a win or draw after every move  |
| **Board state**  | Stores the current 3x3 grid (X, O, or empty), shared by the engine and the AI  |
| **AI engine**    | Runs Minimax over the board state to choose the computer's best move           |
| **Output module**| Displays the board after each move and announces the final result              |

### Level 3 – AI Engine components

- **Move generator:** lists all empty cells the current player can play
- **Terminal test:** checks whether the position is already a win or a draw
- **Evaluator:** scores a finished game (+1 / 0 / −1)
- **Move selector:** picks the highest-scoring move for the AI, assuming the player minimizes

### Level 4 – Code

| Function                                  | Purpose                                                            |
|-------------------------------------------|--------------------------------------------------------------------|
| `print_board(board)`                      | Displays the 3x3 grid after every move                             |
| `check_winner(board)`                     | Returns `'X'`, `'O'`, or `None` by checking all 8 winning lines    |
| `is_full(board)`                          | Returns `True` when no empty cells remain (draw check)             |
| `minimax(board, depth, is_maximizing)`    | Recursive search that returns the score of a position              |
| `best_move(board)`                        | Tries every empty cell, calls `minimax`, returns the best cell     |
| `play_game()`                             | Main loop alternating player and AI turns until the game ends      |

## Design Decisions

- **Board as a flat list of 9 cells** (not a 2D array or a `Board` class), which keeps making and undoing moves simple and fast.
- **Minimax**, because the Tic-Tac-Toe game tree is small enough to search fully, giving a perfect, unbeatable AI.
- **`check_winner` separate from `minimax`**, so the game rules stay independent from the AI logic. The AI can later be replaced (e.g. by Alpha-Beta pruning or a random player) without touching the rules.

## Project Structure

```
.
├── tictactoe.py      # Game rules, Minimax AI, and main loop
├── README.md         # This file
└── CONTRIBUTING.md   # How to contribute, and AI contribution disclosure
```

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md).

## AI Disclosure

Parts of this project were created with the help of Claude (Anthropic). See the AI Contribution section in [CONTRIBUTING.md](CONTRIBUTING.md) for details.
