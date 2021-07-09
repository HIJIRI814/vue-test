<template>
  <div id="app">
    <button @click="squareMove('Up')">上へ参ります</button>
    <button @click="squareMove('Down')">下へ参ります</button>
    <button @click="squareMove('Center')">中央です</button>
    <button @click="squareMove('')">非表示</button>
    <transition name="fade">
      <div v-if="isActive" class="square" :class="squareDirection"></div>
    </transition>
  </div>
</template>

<script>
export default {
  name: 'App',
  data: () => {
    return {
      moveUp: false,
      moveDown: false,
      moveCenter: false,
    };
  },
  methods: {
    squareMove(value) {
      switch (value) {
        case 'Up':
          this.moveUp = true;
          this.moveDown = false;
          this.moveCenter = false;
          break;
        case 'Down':
          this.moveUp = false;
          this.moveDown = true;
          this.moveCenter = false;
          break;
        case 'Center':
          this.moveUp = false;
          this.moveDown = false;
          this.moveCenter = true;
          break;
        default:
          this.moveUp = false;
          this.moveDown = false;
          this.moveCenter = false;
          break;
      }
    },
  },
  computed: {
    squareDirection() {
      return {
        squareUp: this.moveUp,
        squareDown: this.moveDown,
        squareCenter: this.moveCenter,
      };
    },
    isActive() {
      return this.moveUp || this.moveDown || this.moveCenter
    },
  },
};
</script>

<style>
#app {
  width: 90%;
  height: 100vh;
  position: relative;
  margin: 0 auto;
}

.square {
  width: 400px;
  height: 200px;
  border: solid 3px #000;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  transition: all 300ms 0s ease;
}

.squareCenter {
  width: 100px;
  height: 50px;
}
.squareUp {
  width: 600px;
  height: 200px;
  top: 20%;
}
.squareDown {
  top: 80%;
}
.fade-enter-active {
  animation: fade-in 0.5s;
}
.fade-leave-active {
  animation: fade-in 0.5s reverse;
}
@keyframes fade-in {
  0% {
    opacity: 0;
  }
  100% {
    opacity: 1;
  }
}
</style>
