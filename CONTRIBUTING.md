# Contributing

Thanks for your interest in the Tic-Tac-Toe Minimax AI! This document explains how to contribute, and records who (and what) contributed to the project so far.

## AI Contribution Note

### AI tools used

Claude (Anthropic): used for code generation, diagram creation, and document formatting.

### What AI helped with

- Writing and refining the Tic-Tac-Toe and Minimax code
- Drawing the Context, Container, and Component (C4) diagrams
- Formatting the SLE-3 report

### What the author did

- Chose Tic-Tac-Toe as the project
- Defined the Input / Game Engine / Board State / AI Engine / Output breakdown
- Decided which container to expand at the Component level
- Reviewed all AI-generated code and diagrams for correctness
- Wrote the design-decision justification

If you use an AI tool for a contribution, please add a short note to your pull request saying what it helped with, and make sure you have reviewed and understood everything you submit.

## Ways to Contribute

- Report bugs (e.g. invalid input not handled, wrong win/draw detection)
- Add **Alpha-Beta pruning** to `minimax`
- Add a difficulty setting (e.g. random or depth-limited AI)
- Let the player choose to go first or second, or pick X or O
- Add automated tests for `check_winner`, `is_full`, and `best_move`
- Improve documentation or diagrams

## Getting Started

1. Fork the repository and clone your fork.
2. Create a branch from `main`:
   ```bash
   git checkout -b feature/short-description
   ```
3. Make your changes and run the game to check they work:
   ```bash
   python tictactoe.py
   ```
4. Commit, push, and open a pull request.

## Guidelines

### Keep the architecture intact

The design deliberately separates **game rules** (`check_winner`, `is_full`, board state) from **AI logic** (`minimax`, `best_move`). Please keep that separation, so the AI can be replaced without changing the rules.

### Code style

- Follow [PEP 8](https://peps.python.org/pep-0008/)
- Use clear names and short docstrings for functions
- Keep the board as a flat list of 9 cells unless there is a strong reason to change it
- Do not add external dependencies without discussing it first

### Testing

Before submitting, check at least that:

- The AI never loses (play several games, including against random moves)
- All 8 winning lines are detected for both `X` and `O`
- A full board with no winner is reported as a draw
- Invalid input (non-numbers, out-of-range numbers, occupied cells) is rejected without crashing

### Commit messages

Use short, imperative messages, e.g. `Add alpha-beta pruning to minimax`.

### Pull requests

- Keep each PR focused on one change
- Describe what changed and why
- Mention any AI assistance used
- Update `README.md` if behavior or structure changes

## Reporting Issues

Open an issue with:

- What you expected to happen
- What actually happened
- Steps to reproduce (including the moves you played)
- Your Python version and operating system

## Code of Conduct

Be respectful and constructive. Feedback should focus on the work, not the person.
