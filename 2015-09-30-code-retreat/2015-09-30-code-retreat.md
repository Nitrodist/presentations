# [fit] Conway's Game of Life

---

# It's a 'game'

---

```

'-' are dead cells
'#' are alive cells

Turn 1      Turn 2      Turn 3
-------     -------     -------
----#--     ---#---     -------
--##---  →  ---#---  →  -------
-------     -------     -------
```

---

# Still life

![inline 60%](https://upload.wikimedia.org/wikipedia/commons/thumb/9/96/Game_of_life_block_with_border.svg/600px-Game_of_life_block_with_border.svg.png)

---

# 'Spinner'

![inline 150%](https://upload.wikimedia.org/wikipedia/commons/9/95/Game_of_life_blinker.gif)

---

# [gif of the game at scale](https://upload.wikimedia.org/wikipedia/commons/e/e5/Gospers_glider_gun.gif)

---

Format:

1. Pair programming (new partner)
2. 45 minutes to work
3. 5-10 minutes to talk about it
4. Delete your code after
5. Use TDD, clean code, DRY, etc.

---

## https://github.com/k00ka/game-of-life
## http://bit.ly/1O332wL
## one oh three three  two w L

---

4 Rules:

1. Any live cell with fewer than two live neighbours dies, as if caused by under-population.
1. Any live cell with two or three live neighbours lives on to the next generation.
1. Any live cell with more than three live neighbours dies, as if by over-population.
1. Any dead cell with exactly three live neighbours becomes a live cell, as if by reproduction.

---

```
git clean -f
git reset --hard
```
