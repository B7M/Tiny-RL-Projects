# Tiny_RL_Projects

Small reinforcement learning projects built for fun and practice. More coming over time.

---

## 1. Q-Learning: Maze Solver

An off-policy Q-learning agent that learns to navigate a randomly blocked grid maze using a custom Pygame environment (no OpenAI Gym).

### Environment

- **Grid:** 200 x 300 pixels, divided into fixed-size cells
- **Start:** Bottom center of the grid
- **Goal:** Reach the top row (Nirvana)
- **Obstacles:** Randomly placed blocks whose count and positions control difficulty

### Rewards

| State | Reward |
|-------|--------|
| Top row (goal) | +10 |
| Any path cell | -1 per step |
| Block (wall) | -100 |

The agent stays in place if it tries to move into a wall or out of bounds.

### Algorithm

Standard tabular Q-learning with an epsilon-greedy policy:

- **Q-table:** Initialized to zeros; shape `(4 actions, rows, cols)`
- **Actions:** Up, Down, Left, Right
- **Learning rate:** 0.9
- **Discount factor:** 0.9
- **Epsilon:** 0.95 (mostly greedy; 5% random exploration)
- **Episodes:** 25

Update rule:

```
Q(s, a) <- Q(s, a) + lr * [r + gamma * max_a' Q(s', a') - Q(s, a)]
```

### Files

| File | Description |
|------|-------------|
| `maze.py` | Main game loop; supports both `'human'` and `'ai'` player modes |
| `ai.py` | Q-learning agent: reward table, action selection, state transitions, learning loop |
| `video.py` | Assembles saved PNG frames into an animated GIF (`animation.gif`) |
| `maze_objects.py` | Pygame sprite definitions for the agent and blocks (not included here) |

### Output

Each episode saves PNG screenshots of every step and a final win frame. `video.py` stitches these into a GIF with variable frame durations (faster during navigation, slower on win frames).

### Usage

```bash
python maze.py
```

Set `self.player = 'human'` in `Maze.__init__` to control the agent manually with keyboard input.