# **DNDGR Benchmark Levels:**

## **Level 1: 1D Sequence Prediction (Easiest)**

*   **Dimensionality:** 1D (a list)
*   **Grid Size:** N = 100 words
*   **Vocabulary:** Randomly assigned words (or can be defined for specific tasks).
*   **In-Context Examples:**
    *   Start with 10 in-context examples.
    *   Increase incrementally (e.g., by 10 examples at a time) up to a maximum of 1000 examples.
    *   Each example is a sequence of 10 words.
*   **Sequence Generation:**
    *   Start at a random word in the list.
    *   Move to an adjacent word (+1 or -1 index) at each step.
*   **Task:** Predict the next word in a given sequence.
*   **Evaluation:**
    *   Accuracy of next word prediction.
    *   Number of examples needed to reach a target accuracy (if applicable).
    *   Learning curve (accuracy vs. number of examples).

## **Level 2: 2D Sequence Prediction**

*   **Dimensionality:** 2D (a grid)
*   **Grid Size:** N = 10 (10x10 grid)
*   **Vocabulary:** Randomly assigned words.
*   **In-Context Examples:**
    *   Start with 10 in-context examples.
    *   Increase incrementally up to a maximum of 1000 examples.
    *   Each example is a sequence of 10 words.
*   **Sequence Generation:**
    *   Start at a random cell in the grid.
    *   Move to an adjacent cell (up, down, left, or right) at each step.
*   **Task:** Predict the next word in a given sequence.
*   **Evaluation:** Same as Level 1.

## **Level 3: 2D Shortest Path**

*   **Dimensionality:** 2D (a grid)
*   **Grid Size:** N = 10 (10x10 grid)
*   **Vocabulary:** Randomly assigned words.
*   **In-Context Examples:** 1000 examples of sequences with 10 words length each.
*   **Task:** Given a start word and an end word, generate the shortest path between them.
*   **Evaluation:**
    *   Success rate (whether a valid path is generated).
    *   Optimality ratio (length of generated path / length of shortest path).
    *   Average path length (for successful trials).

## **Level 4: 2D Diverse Path Generation**

*   **Dimensionality:** 2D (a grid)
*   **Grid Size:** N = 10 (10x10 grid)
*   **Vocabulary:** Randomly assigned words.
*   **In-Context Examples:** 1000 examples of sequences with 10 words length each.
*   **Task:** Given a start word and an end word, generate as many *diverse* paths as possible that:
    *   Have a minimum length of 10 steps.
    *   Do not repeat any steps.
    *   Are different from the in-context examples.
*   **Evaluation:**
    *   Success rate (whether valid paths are generated).
    *   Average path length (for successful trials).
    *   Diversity score (how different the generated paths are from each other and from examples).
    *   Number of unique paths generated.

## **Level 5: 3D Sequence Prediction**

*   **Dimensionality:** 3D (a space)
*   **Grid Size:** N = 10 (10x10x10 space)
*   **Vocabulary:** Randomly assigned words.
*   **In-Context Examples:**
    *   Start with 10 in-context examples.
    *   Increase incrementally up to a maximum of 10,000 examples (or a smaller number depending on context length limits of LLM).
    *   Each example is a sequence of 10 words.
*   **Sequence Generation:**
    *   Start at a random cell in the space.
    *   Move to an adjacent cell (along any of the three axes) at each step.
*   **Task:** Predict the next word in a given sequence.
*   **Evaluation:** Same as Level 1.

## **Level 6 and beyond:**

*   You can continue to increase the complexity by:
    *   Adding more dimensions (4D, 5D, etc.).
    *   Increasing the grid size (N).
    *   Adding noise (movement errors, word swaps).
    *   Introducing more complex movement rules (e.g., diagonal moves, jumps).
    *   Using different types of functions for coordinate-based regression tasks.
    *   Combining pathfinding with constraints, such as adding more minimum steps for Level 4
    *   Combining pathfinding with constraints, such as adding more unvisited cells or maximum steps for Level 4