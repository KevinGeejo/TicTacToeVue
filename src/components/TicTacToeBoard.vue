<template>
  <div class="board">
    <div 
      class="cell" 
      v-for="(cell, index) in board" 
      :key="index" 
      @click="makeMove(index)"
    >
      {{ cell }}
    </div>
    <div v-if="winner" class="status">
      Winner: {{ winner }}
    </div>
    <div v-else-if="isBoardFull" class="status">
      It's a draw!
    </div>
  </div>
</template>

<script>
export default {
  props: {
    currentPlayer: String
  },
  data() {
    return {
      board: Array(9).fill(null),
      winner: null
    };
  },
  computed: {
    isBoardFull() {
      return this.board.every(cell => cell !== null);
    }
  },
  methods: {
    makeMove(index) {
      if (!this.board[index] && !this.winner) {
        this.$set(this.board, index, this.currentPlayer);
        this.$emit('move', index);
        this.checkWinner();
      }
    },
    checkWinner() {
      const winningCombinations = [
        [0, 1, 2],
        [3, 4, 5],
        [6, 7, 8],
        [0, 3, 6],
        [1, 4, 7],
        [2, 5, 8],
        [0, 4, 8],
        [2, 4, 6]
      ];

      for (let combination of winningCombinations) {
        const [a, b, c] = combination;
        if (this.board[a] && this.board[a] === this.board[b] && this.board[a] === this.board[c]) {
          this.winner = this.board[a];
          this.$emit('winner', this.winner);
          break;
        }
      }
    },
    resetBoard() {
      this.board = Array(9).fill(null); // Reset the board
      this.winner = null;               // Reset the winner
    }
  }
};
</script>

<style scoped>
.board {
  display: grid;
  grid-template-columns: repeat(3, 100px);
  grid-gap: 10px;
  margin-left: 450px;
  margin-bottom: 50px;
}

.cell {
  width: 100px;
  height: 100px;
  display: flex;
  align-items: center;
  justify-content: center;
  background-color: #f0f0f0;
  font-size: 2em;
  cursor: pointer;
}

.cell:hover {
  background-color: #ddd;
}

.status {
  margin: 20px;
  font-size: 1.5em;
}
</style>
