<script>
  export let game;
</script>

<style>
  table {
    border-collapse: collapse;
    font-size: 4em;
  }

  td {
    border: 2px solid rgb(77, 7, 7);
    background-color: blanchedalmond;
    text-align: center;
    height: 1.5em;
    width: 1.5em;
  }
</style>

<table>

  <tbody>
    {#each game.board as row, rowIndex}
      <tr>
        {#each row as column, columnIndex}
          <td
            on:click={() => {
              game = game.click(rowIndex, columnIndex);
            }}>
             {column}
          </td>
        {/each}
      </tr>
    {/each}
  </tbody>
</table>
