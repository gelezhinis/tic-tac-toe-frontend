<template>
  <div class="main">
    <PlayStatus :player="this.player" :winner="winner" :isDraw="isDraw" />
    <div class="board">
      <Box
        v-for="(square, index) in squares"
        :key="index"
        :value="square"
        @click="clickSquare(index)"
      />
    </div>
    <Button @click="resetGame" title="Restart" />
    <div>
      <p v-if="gameWinner">Last Winner - {{gameWinner}}</p>
      <p v-else-if="isDraw">Last Winner - Draw</p>
      <div v-for="(log, index) in logs" :key="index" class="logs">
        <p>Board Log - {{log.boardLog}}</p>
      </div>
    </div>
  </div>
  <teleport to="#modals" v-if="showModal">
    <Modal :winner="winner" :isDraw="isDraw" @click="resetGame" /> 
  </teleport>
</template>

<script>
import Box from './Box.vue';
import PlayStatus from './PlayStatus.vue';
import Button from './Button.vue';
import Modal from './Modal.vue';
import getWinner from '../utils/winner';

export default {
  components: { Box, PlayStatus, Button, Modal },
  data() {
    return {
      player: 'X',
      squares: Array(9).fill(null),
      logs: [],
      gameWinner: null,
      showModal: false
    };
  },
  computed: {
    winner() {
      return getWinner(this.squares);
    },
    isDraw() {
      return this.squares.filter((square) => !square).length === 0;
    },
  },
  methods: {
    async clickSquare(index) {
      if (this.squares[index]) {
        return;
      }
      this.squares.splice(index, 1, this.player);
      this.player = this.player === 'X' ? 'O' : 'X';
      if (this.winner) {
        this.gameWinner = this.winner;
      }

      try {
        await fetch('http://localhost:3000', {
          method: 'POST',
          headers: {
            'Content-Type': 'application/json'
          },
          body: JSON.stringify({
            board: this.squares,
            player: this.player,
            winner: this.gameWinner
          })
        });

        const getResponse = await fetch('http://localhost:3000');
        const getResponseData = await getResponse.json();
        this.logs = getResponseData.reverse();
      } catch(err) {
        console.log(err);
      }
      
      if (this.winner || this.isDraw) {
        this.showModal = true;
        return;
      }

      this.$session.set('board', JSON.stringify(this.squares));
      this.$session.set('player', this.player);
    },
    resetGame() {
      this.player = 'X';
      this.squares.fill(null);
      this.showModal = false;
      this.$session.set('board', JSON.stringify(this.squares));
    }
  },
  async mounted() {
    if (this.$session.get('board') === null && this.$session.get('player') === null) {
      return;
    }
    this.squares = this.$session.get('board');
    this.player = this.$session.get('player');
  }
};
</script>

<style>
.main {
  display: flex;
  flex-direction: column;
  align-items: center;
}
.board {
  display: grid;
  grid-template: repeat(3, 1fr) / repeat(3, 1fr);
  width: 400px;
  height: 400px;
  background-color: #fff;
  color: #fff;
  border-radius: 10px;
}
.logs {
  width: 520px;
  border: 1px solid #666;
}
</style>
