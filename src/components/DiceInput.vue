<template>
  <div class="root">
    <div class="input">
      <span class="common-txt">
        Input dice to roll:
      </span>
      <input
        type="text"
        class="dice-input"
        v-model="diceTextInput"
        @keyup="this.parseText"
        placeholder="Roll me some dice!"
      />
    </div>
    <div class="range">
      <span class="result-range" v-if="diceTextInput!==''">
        {{ minRange }} - {{ maxRange }}
      </span>
      <span class="common-txt">
        :Range
      </span>
    </div>
    <div class="roll-results">
      <span class="common-txt">
        Dice roll results:
      </span>
      <input
        type="text"
        class="dice-output"
        v-model="diceTextOutput"
        readonly
      />
    </div>
    <div class="total">
      <span class="dice-total" v-if="diceTextOutput!==''">
        {{ total }}
      </span>
      <span class="common-txt">
        :Total
      </span>
    </div>
  </div>
</template>

<script>
export default {
  name: 'DiceInput',
  data() {
    return {
      diceTextInput: '',
      diceTextOutput: '',
      minRange: 0,
      maxRange: 0,
      total: 0,
    };
  },
  methods: {
    // This is a very bad placeholder and should be removed immediately!
    parseText() {
      const d = Number.parseInt(this.diceTextInput, 10);
      this.minRange = 1;
      this.maxRange = d;
      this.diceTextOutput = '25';
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
