# Chess Notation (Algebraic Notation)

## Purpose

Chess notation (also called **algebraic notation**) is the standard way to record chess games.

---

# Board Coordinates

The chessboard is labeled with:

- **Files:** `a`–`h` (columns)
    
- **Ranks:** `1`–`8` (rows)
    

Every square has a unique name:  
`a1`, `e4`, `h8`, etc.

---

# Piece Symbols

|Piece|Letter|
|---|---|
|King|`K`|
|Queen|`Q`|
|Rook|`R`|
|Bishop|`B`|
|Knight|`N`|
|Pawn|_(no letter)_|

Examples:

- `e4` → pawn to e4
    
- `Nf3` → knight to f3
    
- `Bb5` → bishop to b5
    

---

# Captures

Use **`x`**.

Examples:

- `Nxe5` → knight captures on e5.
    
- `Bxh7` → bishop captures on h7.
    
- `exd5` → pawn from the **e-file** captures on d5.
    

---

# Check and Checkmate

- `+` = check
    
- `#` = checkmate
    

Examples:

- `Qh5+`
    
- `Qh7#`
    

---

# Castling

- Kingside: `O-O`
    
- Queenside: `O-O-O`
    

---

# Promotion

When a pawn reaches the last rank:

- `e8=Q`
    
- `a1=N`
    

Promotion can be to a queen, rook, bishop, or knight.

---

# En Passant

Usually written just like a normal capture:

`exd6`

Sometimes books add **e.p.**, but this is optional.

---

# Disambiguation

If two identical pieces can move to the same square, specify which one moves.

Examples:

- `Nbd2` → knight from the **b-file** goes to d2.
    
- `R1e1` → rook from **rank 1** goes to e1.
    

---

# Move Numbers

Moves are written in pairs.

```
1. e4 e5
2. Nf3 Nc6
3. Bb5 a6
```

White moves first, then Black.

---

# Annotations

|Symbol|Meaning|
|---|---|
|`!`|Good move|
|`!!`|Brilliant move|
|`?`|Mistake|
|`??`|Blunder|
|`!?`|Interesting move|
|`?!`|Dubious move|

Examples:

- `Nf3!`
    
- `Qh5?`
    
- `Rxe7!!`
    

---

# Game Results

|Result|Meaning|
|---|---|
|`1-0`|White wins|
|`0-1`|Black wins|
|`½-½`|Draw|
|`*`|Game unfinished or result unknown|

---

# Sample Game

```text
1. e4 e5
2. Nf3 Nc6
3. Bb5 a6
4. Ba4 Nf6
5. O-O Be7
6. Re1 b5
7. Bb3 d6
8. c3 O-O
```

---

# Quick Reference

```
K   King
Q   Queen
R   Rook
B   Bishop
N   Knight
(no letter) Pawn

x   Capture
+   Check
#   Checkmate
O-O   Kingside castling
O-O-O Queenside castling
=Q  Promotion
!   Good move
?   Mistake
1-0 White wins
0-1 Black wins
½-½ Draw
```

---
