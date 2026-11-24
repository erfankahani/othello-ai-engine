# Othello AI Agent — Minimax, Alpha–Beta & Expectimax

**Artificial Intelligence course · Homework 3 (Adversarial Search) · Erfan Kahani**

A complete **Othello (Reversi)** engine in pure Python, with game-playing agents built on classic **adversarial search**: Minimax, Alpha–Beta pruning and a risk-aware Expectimax. The notebook also includes an interactive **Human vs AI** board, so you can play against your own agent.

---

## Features

- **Game engine:** legal move generation, disc flipping in all 8 directions, passes and end-of-game detection.
- **Baseline agents:** `RandomAgent` and `GreedyFlipAgent`, which flips the most discs right away.
- **Custom evaluation function:** `12 × corners + 3 × mobility + 1 × disc difference`.
- **Minimax** search with a depth limit.
- **Alpha–Beta pruning** with corner-first move ordering. It chooses the same moves as Minimax and visits far fewer nodes.
- **Risk-aware Expectimax:** the opponent is a chance node that plays its best move with probability `1 − ε` and blunders uniformly with probability `ε`.
- **Interactive GUI:** play against any agent in Jupyter (`ipywidgets`).

## Evaluation Function

| Feature | Weight | Reason |
|---|---|---|
| Corner control (mine − opponent's) | 12 | A corner disc can never be flipped back |
| Mobility (my legal moves − opponent's) | 3 | More options means more control. More reliable than the disc count during the middle game |
| Disc difference | 1 | Matters mostly at the end of the game |

## Results

Each agent plays **Black** against the **Greedy** agent (White), with seed 2:

| Agent | Depth | Winner | Nodes expanded | Time (s) |
|---|---|---|---|---|
| Minimax | 2 | Agent | 1,729 | 0.48 |
| Alpha–Beta | 2 | Agent | **849** | **0.19** |
| Expectimax (ε = 0.3) | 2 | Agent | 1,729 | 0.40 |
| Minimax | 3 | Agent | 19,486 | 4.95 |
| Alpha–Beta | 3 | Agent | **5,084** | **1.19** |
| Expectimax (ε = 0.3) | 3 | Agent | 19,667 | 5.13 |

*Times were measured on one machine and will differ on yours.*

**Takeaways**
- Alpha–Beta plays **exactly the same game** as Minimax but expands **2–4× fewer nodes**, and the savings grow with depth.
- Expectimax can't prune, because every opponent move contributes to the expected value. It is the most expensive agent.
- The cost grows **exponentially with depth**. The branching factor is largest in the middle of the game, when the most squares are playable.

## Project Structure

```
├── othello_agent.ipynb   # Engine, agents, experiments and the Human vs AI GUI
├── requirements.txt
└── README.md
```

## How to Run

```bash
pip install -r requirements.txt
jupyter notebook othello_agent.ipynb
```

Run the cells from top to bottom. The engine and all agents use only the Python standard library. `ipywidgets` is needed only for the **Human vs AI** section at the end.
