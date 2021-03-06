# Design Tic-Tac-Toe

Design a Tic-tac-toe game that is played between two players on a n x n grid.

You may assume the following rules:

1. A move is guaranteed to be valid and is placed on an empty block.
2. Once a winning condition is reached, no more moves is allowed.
3. A player who succeeds in placing n of their marks in a horizontal, vertical, or diagonal row wins the game.

**Example:**  


```text
Given n = 3, assume that player 1 is "X" and player 2 is "O" in the board.TicTacToe toe = new TicTacToe(3);toe.move(0, 0, 1); -> Returns 0 (no one wins)|X| | || | | |    // Player 1 makes a move at (0, 0).| | | |toe.move(0, 2, 2); -> Returns 0 (no one wins)|X| |O|| | | |    // Player 2 makes a move at (0, 2).| | | |toe.move(2, 2, 1); -> Returns 0 (no one wins)|X| |O|| | | |    // Player 1 makes a move at (2, 2).| | |X|toe.move(1, 1, 2); -> Returns 0 (no one wins)|X| |O|| |O| |    // Player 2 makes a move at (1, 1).| | |X|toe.move(2, 0, 1); -> Returns 0 (no one wins)|X| |O|| |O| |    // Player 1 makes a move at (2, 0).|X| |X|toe.move(1, 0, 2); -> Returns 0 (no one wins)|X| |O||O|O| |    // Player 2 makes a move at (1, 0).|X| |X|toe.move(2, 1, 1); -> Returns 1 (player 1 wins)|X| |O||O|O| |    // Player 1 makes a move at (2, 1).|X|X|X|
```

**Follow up:**  
Could you do better than O\(n2\) per `move()` operation?

分析

和grid illumination问题一样，4个hashtable, 横竖和2个对角线，一个Player+另一个-

注意先移动再判断

```text
from collections import Counter


class TicTacToe:

    def __init__(self, n: int):
        """
        Initialize your data structure here.
        """
        self.h, self.v, self.l, self.r = Counter(), Counter(), Counter(), Counter()
        self.n = n

    def move(self, row: int, col: int, player: int) -> int:
        """
        Player {player} makes a move at ({row}, {col}).
        @param row The row of the board.
        @param col The column of the board.
        @param player The player, can be either 1 or 2.
        @return The current winning condition, can be either:
                0: No one wins.
                1: Player 1 wins.
                2: Player 2 wins.
        """
        val = 1 if player == 1 else -1
        self.h[row] += val
        self.v[col] += val
        self.l[row+col] += val
        self.r[row-col] += val
        if self.h[row] == self.n or self.h[row] == -self.n or self.v[col] == self.n or self.v[col] == -self.n or self.l[row+col] == self.n or self.l[row+col] == -self.n or self.r[row-col] == self.n or self.r[row-col] == -self.n:
            return player
        return 0

# Your TicTacToe object will be instantiated and called as such:
# obj = TicTacToe(n)
# param_1 = obj.move(row,col,player)
```

```text
class TicTacToe:        def __init__(self, n: int):        """        Initialize your data structure here.        """        self.n = n        self.h,self.v,self.l,self.r = collections.Counter(),collections.Counter(),collections.Counter(),collections.Counter()            def move(self, row: int, col: int, player: int) -> int:        """        Player {player} makes a move at ({row}, {col}).        @param row The row of the board.        @param col The column of the board.        @param player The player, can be either 1 or 2.        @return The current winning condition, can be either:                0: No one wins.                1: Player 1 wins.                2: Player 2 wins.        """        x,y,n = row,col,self.n        val = 1 if player == 1 else -1        self.h[x] += val        self.v[y] += val        self.l[x+y] += val        self.r[x-y] += val        if self.h[x] == n or self.h[x] == -n or self.v[y] == n or self.v[y] == -n or self.l[x+y] == n or self.l[x+y] == -n or self.r[x-y] == n or self.r[x-y] == -n:            return player        return 0
```





