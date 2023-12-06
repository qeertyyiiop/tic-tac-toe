<template>
  <div>
    <div class="text-center">
      <span class="text-4xl font-bold"> Tic-tac-toe </span>
    </div>
    <div
      v-if="!ended"
      class="flex flex-col flex-wrap justify-center gap-8 px-0 py-0 my-12"
    >
      <div
        v-for="(row, rowIndex) in gameBoard"
        :key="rowIndex"
        class="space-x-16 flex items-center justify-center"
      >
        <button
          v-for="(col, colIndex) in row"
          :key="colIndex"
          class="flex items-center justify-center"
          @click="handleClick(rowIndex, colIndex)"
        >
          {{ gameBoard[rowIndex][colIndex] }}
        </button>
      </div>
    </div>
    <div v-else>
      <span>
        Game ended! <br />
        Winner - {{ winner }}
      </span>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      gameBoard: [
        [null, null, null],
        [null, null, null],
        [null, null, null],
      ],
      turnCounter: 0,
      ended: false,
      winner: "",
    };
  },
  computed: {
    currentTurn() {
      return this.turnCounter % 2 == 0 ? "X" : "O";
    },
  },
  methods: {
    handleClick(rowIndex, colIndex) {
      if (this.gameBoard[rowIndex][colIndex] === null) {
        this.gameBoard[rowIndex][colIndex] = this.currentTurn;
        this.turnCounter++;
      }

      let winner = this.checkGameBoard();

      if (winner != "D") {
        this.ended = true;
        this.winner = winner;
      }
      if (this.turnCounter == 9) {
        if (winner == "D") {
          console.log("Draw");
        } else {
          console.log(winner);
        }
      }
    },
    checkGameBoard() {
      for (let i = 0; i < 3; i++) {
        if (
          this.gameBoard[i][0] == this.gameBoard[i][1] &&
          this.gameBoard[i][1] == this.gameBoard[i][2] &&
          this.gameBoard[i][0] !== null
        ) {
          return this.gameBoard[i][0];
        }
      }
      for (let i = 0; i < 3; i++) {
        if (
          this.gameBoard[0][i] == this.gameBoard[1][i] &&
          this.gameBoard[1][i] == this.gameBoard[2][i] &&
          this.gameBoard[2][i] !== null
        ) {
          return this.gameBoard[0][i];
        }
      }
      if (
        this.gameBoard[0][0] == this.gameBoard[1][1] &&
        this.gameBoard[1][1] == this.gameBoard[2][2] &&
        this.gameBoard[2][2] !== null
      ) {
        return this.gameBoard[2][2];
      }
      if (
        this.gameBoard[0][2] == this.gameBoard[1][1] &&
        this.gameBoard[1][1] == this.gameBoard[2][0] &&
        this.gameBoard[2][0] !== null
      ) {
        return this.gameBoard[2][2];
      }
      return "D";
    },
  },
};
</script>

<style scoped>
@import url("https://fonts.googleapis.com/css2?family=Caprasimo&family=Roboto+Slab:wght@400;700&display=swap");
button {
  width: 8rem;
  height: 8rem;
  border: none;
  background: #fff;
  color: #3f3b00;
  font-size: 5rem;
  cursor: pointer;
  font-family: "Caprasimo", cursive;
  padding: 1rem;
}
</style>
