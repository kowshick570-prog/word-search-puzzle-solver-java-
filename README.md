# 🔎 Word Search Puzzle Solver

A Java-based console application that locates a given list of words hidden within a 2D letter grid. The solver scans in all eight directions — horizontal, vertical, and diagonal (forward and reverse) — using a **Depth-First Search (DFS) with backtracking** algorithm.

---

## 📌 Project Information

| Field | Detail |
|---|---|
| **Register Number** | 711524BEE302 |
| **Student Name** | Kowshick K |
| **Project Title** | Word Search Puzzle Solver |
| **Domain** | Low-Level Design (LLD), built on DSA fundamentals |
| **Language** | Java |
| **Core Concepts** | 2D Arrays, Backtracking, OOP (Classes & Objects) |

---

## 📖 Overview

Word search puzzles present a grid of letters in which target words are hidden in any of eight directions. This project implements an object-oriented solution that:

- Represents the puzzle board as a reusable `Grid` object
- Delegates the search logic to a dedicated `WordSearchSolver` class
- Uses recursive backtracking to explore candidate paths, undoing invalid moves as it goes
- Demonstrates **composition** — `WordSearchSolver` holds a `Grid` object rather than extending it

> **Note:** All three classes are combined in a single file (`WordSearchPuzzleSolver.java`) since Java allows only one `public` class per file. `WordSearchPuzzleSolver` is the public driver class; `Grid` and `WordSearchSolver` are package-private classes living in the same file.

---

## 🏗️ System Design

### Class Diagram

```
┌─────────────────────────────────┐          ┌──────────────────────────────────────┐
│              Grid               │          │          WordSearchSolver            │
├---------------------------------|          ├--------------------------------------|
│ - board : char[][]              │          │ - grid : Grid                        │
│ - rows  : int                   │          │ - DIRECTIONS : int[8][2] (static)    |
│ - cols  : int                   │          ├──────────────────────────────────────┤
├─────────────────────────────────┤          │ + WordSearchSolver(grid: Grid)       │
│ + Grid(board: char[][])         │          │ + findWord(word: String): List<int[]>│
│ + getRows(): int                │          │ - backtrack(row, col, word, index,   │
│ + getCols(): int                │          │     visited, path): boolean          │
│ + charAt(row, col): char        │          └──────────────────┬───────────────────┘
│ + isInBounds(row, col): boolean │                             │ creates
│ + print(): void                 │                             │
└──────────────┬──────────────────┘               ┌─────────────┴──────────────┐
               │ creates                          │   WordSearchPuzzleSolver   │
               └──────────────────────────────────┤   + main(args: String[])   │
                                                  └────────────────────────────┘
```

### Responsibilities

| Class | Responsibility |
|---|---|
| **Grid** | Holds the puzzle state (`board`, `rows`, `cols`); exposes safe read access (`charAt`), bounds-checking (`isInBounds`), and a display helper (`print`). |
| **WordSearchSolver** | Holds a `Grid` reference; runs the backtracking search (`findWord`) that scans all cells and all 8 directions to locate a word, returning its coordinate path. |
| **WordSearchPuzzleSolver** *(main)* | Application entry point; builds the board, creates the `Grid` and `WordSearchSolver` objects, and prints results for each search word. |

---

## ⚙️ Algorithm

**`findWord(String word)`**
1. Initialize a `visited[][]` matrix the same size as the grid.
2. Scan every cell `(r, c)`; whenever it matches the word's first character, start a backtracking search from there.
3. **`backtrack(row, col, word, index, visited, path)`**
   - Return `false` if the cell is out of bounds, already visited, or doesn't match `word.charAt(index)`.
   - Mark the cell visited and add it to `path`.
   - If this was the word's last character, the word is found — return `true`.
   - Otherwise, try all 8 `DIRECTIONS` recursively from this cell.
   - If none of the 8 directions succeed, **undo** the visit and remove the cell from `path` (backtrack), then return `false`.
4. Return the first successful `path` found, or an empty list if the word isn't present.

**Directions covered:** up, down, left, right, and all 4 diagonals — `{-1,0} {1,0} {0,-1} {0,1} {-1,-1} {-1,1} {1,-1} {1,1}`.

**Time Complexity:** O(rows × cols × 8^L) worst case per word, where L is the word length (bounded in practice by early mismatches and the `visited` check).

---

## 🚀 Getting Started

### Prerequisites
- Java Development Kit (JDK) 8 or higher

### Build & Run
```bash
javac WordSearchPuzzleSolver.java
java WordSearchPuzzleSolver
```

### Sample Output
```
Grid:
C A T F 
X O D O 
B G D G 
E R A S 

CAT -> FOUND at: (0,0) (0,1) (0,2)
DOG -> FOUND at: (1,2) (1,1) (2,0)
DODGE -> NOT FOUND
BAG -> FOUND at: (2,0) (2,1) (1,1)
```
*(exact coordinates depend on the DFS path taken through the grid)*

---

## 📂 Project Structure

```
word-search-puzzle-solver-java-/
├── docs/
│   ├── class-diagram.png
│   ├── sample-output.txt
│   └── WordSearchPuzzleSolver.java
└── README.md
```

---

## 🧠 Key Concepts Demonstrated

- **2D Array Traversal** — modeling and navigating the letter grid
- **Backtracking (DFS)** — systematically exploring and undoing search paths
- **Object-Oriented Design** — `Grid` and `WordSearchSolver` as collaborating objects (composition), with a clean separation from the driver (`main`)

---

## 🙋 Author

**Kowshick K** — Reg. No. 711524BEE302

---

## 📄 License

This project was developed as part of a Low-Level Design (LLD) Mini Project assignment, built on core Data Structures & Algorithms concepts.
