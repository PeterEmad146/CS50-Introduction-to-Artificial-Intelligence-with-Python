# Tic-Tac-Toe

Using Minimax, implement an AI to play Tic-Tac-Toe optimally.

<div align=center>
<img src="../../../pics/game.png">
</div>

## Getting Started 
- Download the distribution code from <a href ="https://cdn.cs50.net/ai/2023/x/projects/0/tictactoe.zip" style="color:pink">THIS LINK</a> and unzip it.
- Once in the directory for the project, run <code style="color:white">pip3 install -r requirements.txt</code> to install the required Python package (<code style="color:white">pygame</code>) for this project.

## Understanding

There are two main files in this project: <code style="color:white">runner.py</code> and <code style="color:white">tictactoe.py</code>. <code style="color:white">tictactoe.py</code> contains all of the logic for playing the game, and for making optimal moves. <code style="color:white">runner.py</code> has been implemented for you, and contains all of the code to run the graphical interface for the game. Once you've completed all the required functions in <code style="color:white">tictactoe.py</code>, you should be able to run <code style="color:white">python runner.py</code> to play against your AI!

Let's open up <code style="color:white">tictactoe.py</code> to get an understanding for what's provided. First, we define three variables: <code style="color:white">X</code>, <code style="color:white">O</code>, and <code style="color:white">EMPTY</code>, to represent possible moves of the board.

The function <code style="color:white">initial_state</code> returns the starting state of the board. For this problem, we've chosen to represent the board as a list of three lists (representing hte three rows of the board), where each internal list contains three values that are either <code style="color:white">X</code>, <code style="color:white">O</code>, or <code style="color:white">EMPTY</code>. What follows are functions that we've left up to you to implement!

## Specification

Complete the implementation of <code style="Color:white">player</code>, <code style="Color:white">actions</code>, <code style="Color:white">result</code>, <code style="Color:white">winner</code>, <code style="Color:white">terminal</code>, <code style="Color:white">utility</code>, and <code style="Color:white">minimax</code>.

- The <code style="Color:white">player</code> function should take a <code style="Color:white">board</code> state as input, and return which player's turn it is (either <code style="Color:white">X</code> or <code style="Color:white">O</code>).
    - In the initial game state, <code style="Color:white">X</code> gets the first move. Subsequently, the player alternates with each additional move.
    - Any return value is acceptable if a terminal board is provided as input (i.e., the game is already over).
- The <code style="Color:white">actions</code> function should return a <code style="Color:white">set</code> of all of the possible actions that can be taken on a given board.
    - Each action should be represented as a tuple <code style="Color:white">(i, j)</code> where <code style="Color:white">i</code> corresponds to the row of the move (<code style="Color:white">0</code>, <code style="Color:white">1</code>, or <code style="Color:white">2</code>) and <code style="Color:white">j</code> corresponds to which cell in the row corresponds to the move (also <code style="Color:white">0</code>, <code style="Color:white">1</code>, or <code style="Color:white">2</code>).
    - Possible moves are any cells on the board that do not already have an <code style="Color:white">X</code> or an <code style="Color:white">O</code> in them.
    - Any return value is acceptable if a terminal board is provided as input.
- The <code style="Color:white">result</code> function takes a <code style="Color:white">board</code> and an <code style="Color:white">action</code> as input, and should return a new board state, without modifying the original board.
    - If <code style="Color:white">action</code> is not a valid action for the board, your program should raise an exception.
    - The returned board state should be the board that would result from taking the original input board, and letting the player whose turn it is make their move at the cell indicated by the input action.
    - Importantly, the original board should be left unmodified: since Minimax will ultimately require considering many different board states during its computation. This means that simply updating a cell in <code style="Color:white">board</code> itself is not a correct implementation of the <code style="Color:white">result</code> function. You'll likely want to make a deep copy of the board first before making any changes.
- The <code style="Color:white">winner</code> function should accept a <code style="Color:white">board</code> as input, and return the winner of the board if there is one.
    - If the X player has won the game, your function should return <code style="Color:white">X</code>. If the O player has won the game, your function should return <code style="Color:white">O</code>.
    - One can win the game with three of their moves in a row horizontally, vertically, or diagonally.
    - You may assume that there will be at most one winner (that is, no board will ever have both players with three-in-a-row, since that would be an invalid board state).
    - If there is no winner of the game (either because the game is in progress, or because it ended in a tie), the function should return <code style="Color:white">None</code>.
- The <code style="Color:white">terminal</code> function should accept a <code style="Color:white">board</code> as input, and return a boolean value indicating whether the game is over.
    - If the game is over, either because someone has own the game or because all cells have been flled without anyone winning, the function should return <code style="Color:white">True</code>.
    - Otherwise, the function should return <code style="Color:white">False</code> if the game is still in progress.
- The <code style="Color:white">utility</code> function should accept a terminal <code style="Color:white">board</code> as input and output the utility of the board.
    - If X has won the game, the utility is <code style="Color:white">1</code>. If 0 has won the game, the utility is <code style="Color:white">-1</code>. If the game has ended in a tie, the utility is <code style="Color:white">0</code>.
    - Yoy may assume <code style="Color:white">utility</code> will only be called on a <code style="Color:white">board</code> if <code style="Color:white">terminal(board)</code> is <code style="Color:white">True</code>.
- The <code style="Color:white">minimax</code> function should take a <code style="Color:white">board</code> as input, and return the optimal move for the player to move on that board.
    - The move returned should be the optimal action <code style="Color:white">(i, j)</code> that is one of the allowable actions on the board. If multiple moves are equally optimal, any of those moves is acceptable.
    - If the <code style="Color:white">board</code> is a terminal board, the <code style="Color:white">minimax</code> function should return <code style="Color:white">None</code>.

For all functions that accept a <code style="Color:white">board</code> as input, you may assume that it is a valid board (namely, that it is a list that contains three rows, each with three values of either <code style="Color:white">X</code>, <code style="Color:white">O</code>, or <code style="Color:white">EMPTY</code>). You should not modify the function declarations (the order or number of arguments to each function) provided.

Once all functions are implemented correctly, you should be able to run <code style="Color:white">python runner.py</code> and play against your AI. And, since Tic-Tac-Toe is a tie given optimal play by both sides, you should never be able to beat the AI (though if you don't play optimally as well, it may beat you!)

## Hints

- If you'd like to test your functions in a different Python file, you can import them with lines like <code style="Color:white">from tictactoe import initial_state</code>.
- You're welcome to add additional helper functions to <code style="Color:white">tictactoe.py</code>, provided that their names do not collide with function or variable names already in the module.
- Alpha-beta pruning is optimal, but may make your AI run more efficiently!

## Testing

If you'd like, you can execute the below (after setting up <a href="https://cs50.readthedocs.io/projects/check50/en/latest/index.html" style="color:pink">check50</a> on your system) to evaluate the correctness of your code. This isn't obligatory; you can simply submit following the steps at the end of this specification, and these same tests will run on our server. Either way, be sure to compile and test it yourself as well!

```
check50 ai50/projects/2024/x/tictactoe
```

Execute the below to evaluate the style of your code using <code style="color:white">style50</code>.

```
style50 tictactoe.py
```

<div align=center>
&copy; CS50 AI - Harvard University
</div>