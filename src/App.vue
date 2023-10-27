<template>
  <h1>Ninja Reaction Timer</h1>

  <div class="mt-50">
    <button class="app-button" @click="start()" :disabled="showModal"><b>Play</b></button>
  </div>

  <teleport to=".modals" v-if="showModal">
    <Block :showModal="showModal" :blockType="blockType" :delay="delay" @end="endGame" @closeEvent="toggleModal">
      <div><b>CLICK HERE!</b></div>
    </Block>
  </teleport>

  <div class="mt-50"><Result :score="score" v-if="score"></Result></div>
</template>

<script>
import Block from './components/Block.vue';
import Result from './components/Result.vue';

export default {
  name: 'App',
  data() {
    return {
      blockType: 'reaction_block',
      showModal: false,
      delay: null,
      score: null
    }
  },

  components: { Block, Result },

  methods: {
    toggleModal() {
      this.showModal = !this.showModal;
    },

    start() {
      this.delay = 2000 + Math.random() * 5000;
      this.showModal = true;
      console.log(this.delay);
    },

    endGame(reactionTime) {
      this.score = reactionTime;
      console.log('SCORE: ', this.score);
      this.showModal = false;
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #444;
  margin-top: 60px;
}
body { margin: 0; }
.app-button { font-size: 17px; padding: 10px 20px; background-color: slateblue; color: #FFF; border: 0; border-radius: 10px; cursor: pointer; }
.app-button:hover { opacity: 0.77; }
.mt-50 { margin-top: 50px; }
.fs-20 { font-size: 20px; }
</style>
