<template>
  <div id="app">
    <h1 class="heading">Tic Tac Toe</h1>
    <TicTacToeBoard 
      ref="board" 
      :currentPlayer="currentPlayer" 
      @move="handleMove" 
      @winner="winner = $event" 
    />
    <button class="restart-btn" @click="resetGame">Restart Game</button>
  </div>
</template>

<script>
import TicTacToeBoard from './components/TicTacToeBoard.vue';

export default {
  components: {
    TicTacToeBoard
  },
  data() {
    return {
      currentPlayer: 'X',
      winner: null
    };
  },
  methods: {
    handleMove() {
      if (!this.winner) {
        this.currentPlayer = this.currentPlayer === 'X' ? 'O' : 'X';
      }
    },
    resetGame() {
      this.$refs.board.resetBoard(); // Call resetBoard on the child component
      this.currentPlayer = 'X';      // Reset the current player
      this.winner = null;            // Reset the winner in parent component
    }
  }
};
</script>

<style>
#app {
  text-align: center;
  background-color: #ffe6e6; /* Light gray background */
  ; /* Ensure it covers the full height of the page */
   /* Add some padding at the top */
   /* Add some padding at the bottom */
  height : 100vh;
  flex-direction: column;
  
  align-items: center;
}

.heading{
  margin-top: 1%;
  margin-bottom: 5%;
  font-size: 30px;
  font-family:'Courier New', Courier, monospace;
}

.restart-btn {
  background-color:#4CAF50;
  color: white;
  border: none;
  padding: 15px 32px;
  font-size: 16px;
  font-weight: bold;
  margin-top: 20px;
  cursor: pointer;
  border-radius: 10px;
  transition: background-color 0.3s ease, transform 0.2s ease;
}

.restart-btn:hover {
  background-color: #45a049;
  transform: scale(1.05);
}

.restart-btn:active {
  background-color: #388e3c;
  transform: scale(1);
}
</style>
