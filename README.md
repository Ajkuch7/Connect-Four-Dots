# Connect Four AI

This repository implements a Connect Four game with an AI opponent using a bitboard representation and depth‑limited minimax search. The project includes a Pygame GUI, a headless runner for automated matches, and simple instrumentation so you can compare Alpha‑Beta pruning vs plain minimax.

Key features

- Bitboard board representation (compact and fast bitwise win checks)
- Minimax with Alpha‑Beta pruning (configurable depth)
- Plain Minimax (no pruning) for comparison
- Headless runner to run AI vs AI matches (`headless_runner.py`)
- Quick metrics test script (`test_metrics.py`) to show nodes explored / time
- Pygame GUI with the ability to choose AI algorithm before play

Note: The GUI borrows images and layout ideas from the "Four in a Row" example but the AI and wiring were implemented as part of this project.

## Requirements

- Python 3.8+ recommended (tested with Python 3.13 and pygame 2.6)
- pygame (modern version; requirements.txt originally pinned an old pygame that may not build on modern toolchains)

Install:

```powershell
python -m pip install -r requirements.txt
# If requirements.txt contains an old pygame and fails to build, install a modern pygame manually, e.g.:
python -m pip install pygame
```

## How to run

GUI (play locally):

```powershell
cd path\to\connect-four-ai
python .\main.py
```

When prompted you can choose the AI algorithm:

- Enter `1` for AlphaBeta (default) — stronger and uses pruning
- Enter `2` for Plain Minimax (no pruning) — useful for comparison / debugging

Headless AI vs AI matches (no GUI):

```powershell
python .\headless_runner.py
```

This runs a small series of automated games (configurable in the file) and prints win counts, average moves and time per move.

Quick metrics (single-position profiling):

```powershell
python .\test_metrics.py
```

Shows nodes explored, nodes pruned (if any), and elapsed time for the searches.

## Files of interest

- `main.py` — entry point and GUI glue; contains the `Game` and `State` classes
- `fourInARowGUI/` — Pygame GUI code and image resources
- `core.py` — (added) pure game/search logic used by headless runner
- `headless_runner.py` — run AI vs AI matches without the GUI
- `test_metrics.py` — quick profiler for node counts and timing
- `requirements.txt` — Python dependencies (may need updating on modern systems)

## Authors

- [Ajay Ajkuch7](https://github.com/Ajkuch7)
- [Aadil shakya](https://github.com/aadilshakya)

## Notes and tips

- Alpha‑Beta pruning does not change the chosen move if both searches run to the same depth — it only prunes irrelevant subtrees and therefore runs faster or enables deeper search in the same time budget.
- If you plan to run many automated matches or increase depths, prefer running the headless runner so the GUI does not slow the experiment.
- If you want me to add Negamax+transposition table or an MCTS player, I can implement and wire them into the headless runner for direct comparisons.

If anything in this README should be more specific to your workflow (different Python path, extra scripts, or CI instructions), tell me and I'll update it.
