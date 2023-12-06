<template>
  <div class="scores">
    <span :class="{ active: game.sign === game.signX }">
      X score: {{ game.xScore }}
    </span>
    <span :class="{ active: game.sign === game.signO }">
      O Score: {{ game.oScore }}
    </span>
  </div>
</template>

<script>
import { mapGetters } from 'vuex';

export default {
  computed: {
    ...mapGetters('game', [
      'cells',
      'crossClass',
      'finished',
      'message',
      'oScore',
      'messageStatus',
      'sign',
      'signO',
      'signX',
      'started',
      'winningOrder',
      'winningOrders',
      'xScore',
    ]),
    game() {
      return {
        cells: this.cells,
        crossClass: this.crossClass,
        finished: this.finished,
        message: this.message,
        oScore: this.oScore,
        messageStatus: this.messageStatus,
        sign: this.sign,
        signO: this.signO,
        signX: this.signX,
        started: this.started,
        winningOrder: this.winningOrder,
        winningOrders: this.winningOrders,
        xScore: this.xScore,
      };
    },
  },
};
</script>

<style scoped>
.scores {
  display: flex;
  justify-content: space-around;
  width: 360px;
  padding: 12px;
  background-color: whitesmoke;
  margin-bottom: 22px;
  font-size: 22px;
  border-radius: 6px;
}
.scores .active {
  cursor: default;
  color: #0e980e;
  font-weight: bold;
}
</style>
