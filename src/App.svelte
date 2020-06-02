<script>
  import NewBoard from "./board.svelte";
  

  let message;
  let game = createGame();

  function createGame() {
    message = null;

    return new TicTacToe({
      Win(winner) {
        message = `${winner} wins!`;
      },

      Tie() {
        message =  "Game Draw!"
      }
    });
  }

  function newGame() {
    game = createGame();
  }

    function TicTacToe({ Win, Tie }) {
	const board = [['', '', ''], ['', '', ''], ['', '', '']];

	let turn = 'X';
	let done = false;

	return {
		board,

		click(rowIdx, colIdx) {
			if (!done && !board[rowIdx][colIdx]) {
				board[rowIdx][colIdx] = turn;
				turn = turn === 'X' ? 'O' : 'X';

				const winner = getWinner(board);

				if (winner) {
					Win(winner);
					done = true;
				} else if (isBoardFull(board)) {
					Tie();
					done = true;
				}
			}

			return this;
		}
	};
}

function getWinner(board) {
	for (let row = 0; row < 3; row++) {
		if (
			board[row][0] === board[row][1] &&
			board[row][0] === board[row][2]
		) {
			return board[row][0];
		}
	}

	for (let column = 0; column < 3; column++) {
		if (
			board[0][column] === board[1][column] &&
			board[0][column] === board[2][column]
		) {
			return board[0][column];
		}
	}

	if (board[0][0] === board[1][1] && board[0][0] == board[2][2]) {
		return board[0][0];
	}

	if (board[0][2] === board[1][1] && board[0][2] == board[2][0]) {
		return board[0][2];
	}
}

function isBoardFull(board) {
	for (let row = 0; row < 3; row++) {
		for (let column = 0; column < 3; column++) {
			if (!board[row][column]) {
				return false;
			}
		}
	}

	return true;
}

</script>

<style>
  h2 {
    display: inline;
  }

  .container{
    margin: auto;
  width: 50%;
  border: 3px solid rgb(77, 7, 7);;
  padding: 10px;
  }

  .board-class{
    margin: auto;
  width: 50%;
  }
</style>

<svelte:head>
	<title>Tic Tac Toe</title>
</svelte:head>

<div class="container">



<div class="board-class">
<h1>Tic Tac Toe</h1>
<NewBoard {game} />
</div>
<br>
<hr>
Results:
{#if message}
  <h2>{message}</h2>
{/if}
<hr>
{#if message}
<button on:click={newGame}>New Game</button>
{/if}

</div>
