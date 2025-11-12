# PSA_Final_Project

# Monte Carlo Tree Search for Nim

An AI agent implementing Monte Carlo Tree Search (MCTS) algorithm to play optimal Nim strategy, achieving 95%+ win rates through UCT selection and nim-sum heuristic optimization.

## Project Overview

This project extends a Monte Carlo Tree Search framework to the game of Nim, demonstrating how MCTS converges toward optimal play when enhanced with domain-specific heuristics. Through comprehensive experimental analysis across multiple heap configurations and simulation budgets, we validate that increased computational effort leads to near-perfect strategic play.

**Key Achievement:** MCTS agent achieves 100% win rate in favorable positions and correctly identifies losing positions, aligning perfectly with game theory predictions.

---

## Performance Results

**Key Findings:**
- **Winning positions (nim-sum ≠ 0):** MCTS wins 95-100% with sufficient simulation budget
- **Losing positions (nim-sum = 0):** Win rate correctly approaches 0%
- **vs Random agent:** 60-90% win rate depending on position complexity
- **Budget impact:** Higher simulation counts yield convergence to optimal strategy

*For detailed performance charts and experimental data, see the "Nim_Reports" folder.*

---

## Game Rules: Nim

- **Setup:** Multiple heaps with objects (e.g., [1, 3, 5, 7])
- **Gameplay:** Players alternate removing objects from a single heap
- **Victory:** Player who removes the last object wins
- **Strategy:** Determined by nim-sum (XOR of all heap sizes)
  - Nim-sum ≠ 0 → Current player can force a win
  - Nim-sum = 0 → Current player in losing position

---

##  MCTS Implementation

### Four Core Phases

**1. Selection**
- Traverse tree using UCT (Upper Confidence Bound for Trees)
- Balance exploration vs exploitation with C = √2

**2. Expansion**
- Add unexplored child nodes to the search tree

**3. Simulation (Rollout)**
- Play random game to terminal state
- **Enhanced with nim-sum heuristic:**
  - If nim-sum ≠ 0: Play optimal move to zero it
  - If nim-sum = 0: Play first legal move

**4. Backpropagation**
- Update win/playout counts up the tree

### Heuristic Enhancement

The zero-XOR heuristic dramatically improves convergence:
- Reduces noise from random simulations
- Ensures rollouts follow perfect-play strategy
- Accelerates learning in solvable positions

---

##  Architecture

**Modular Design:**
- Core interfaces: `Game`, `State`, `Move`, `Node`
- Nim-specific implementations: `NimGame`, `NimState`, `NimMove`, `NimNode`
- Plug-in architecture allows extension to other turn-based games

**Key Classes:**
- `NimNode` - Tracks wins and playouts for tree nodes
- `UCT` - Selection algorithm balancing exploration/exploitation
- `NimExperiment` - Automated testing framework

---

##  Getting Started

### Prerequisites
- Java 11+
- Maven 3.6+


## xperimental Setup

### Tested Configurations

**Heap Configurations:**
- [1, 2] - Simple winning position
- [1, 3, 5, 7] - Classic Nim start (losing position)
- [2, 2, 2, 2] - Symmetrical configuration
- [3, 4, 5] - Complex winning position
- [5, 5, 5] - Symmetrical winning position

**Simulation Budgets:**
- MCTS(500) vs MCTS(100)
- MCTS(500) vs MCTS(0) - vs Random
- MCTS(500) vs MCTS(500)
- MCTS(0) vs MCTS(500) - Random vs MCTS
- MCTS(500) vs MCTS(5000) - High budget comparison

**Methodology:**
- 1,000 games per configuration
- Alternating first player to mitigate bias
- CSV logging of results and runtime

---

## Key Insights

### Configuration Analysis

**[1, 2] - Winning Start:**
- Nim-sum = 3 (nonzero) → P0 should win
- **Result:** P0 wins 100% (perfect convergence)

**[1, 3, 5, 7] - Losing Start:**
- Nim-sum = 0 → P0 should lose
- **Result:** P0 win rate 26-50% (depends on opponent strength)
- Demonstrates correct identification of losing position

**[3, 4, 5] - Complex Winning:**
- Nim-sum ≠ 0 but requires deeper search
- **Result:** 78-99% win rate (higher budget = better performance)

### Impact of Simulation Budget

- **Low budget (100):** Can miss optimal moves in complex positions
- **Medium budget (500):** Strong performance, near-optimal
- **High budget (5000):** Converges to perfect play

---

## Technical Highlights

- **Game Theory Integration:** Nim-sum heuristic based on Sprague-Grundy theorem
- **Statistical Validation:** Experimental results align with mathematical predictions
- **Scalable Architecture:** Extensible to other combinatorial games
- **Performance Optimization:** Efficient tree traversal and state management

---

## 📖 Full Documentation

For complete methodology, experimental results, performance charts, and detailed analysis, see the **[Nim_Reports](Final Report .pdf/)** folder.

---

## Team Project

This project was developed collaboratively for **Data Structures, Algorithms & Design Patterns** coursework.

**My Contributions:**
- Implemented UCT selection algorithm
- Developed nim-sum heuristic for optimal play
- Designed and executed comprehensive experimental framework
- Created performance visualizations and statistical analysis
- Wrote technical documentation

*Forked from original course repository to showcase in portfolio*

---

## Future Enhancements

- [ ] Implement transposition tables for efficiency
- [ ] Add support for Misère Nim variant
- [ ] Integrate neural network for evaluation
- [ ] Extend framework to other combinatorial games (Hex, Go)
- [ ] Add real-time visualization of MCTS tree growth

---

**Built with ☕ and Java**
