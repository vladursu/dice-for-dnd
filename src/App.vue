<template>
  <div id="app">
    <DiceInput/>
  </div>
</template>

<script>
import DiceInput from './components/DiceInput.vue';

export default {
  name: 'app',
  components: {
    DiceInput,
  },
};
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
