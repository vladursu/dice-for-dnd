<template>
  <div class="root">
    <div class="input">
      <span class="common-txt">
        Input dice to roll:
      </span>
      <div
        contenteditable
        id="div-input"
        class="dice-input"
        @keyup="this.parseText"
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
import { colours } from '../assets/strings';

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
      const divEl = document.getElementById('div-input');
      this.diceTextInput = divEl.textContent;
      const spanned = this.constructSpans();
      // colour individual letters
      divEl.innerHTML = spanned;
      if (spanned !== '') {
        // set the cursor to the end of the input
        // by default it goes to the start
        this.setCaret();
      }
      console.log('parseText called. input is: ', this.diceTextInput, ' length: ', this.diceTextInput.length);
      const d = Number.parseInt(this.diceTextInput, 10);
      this.minRange = 1;
      this.maxRange = d;
      this.diceTextOutput = '25';
    },
    constructSpans() {
      let spans = '';
      const text = this.diceTextInput;
      const myColors = [colours.d4, colours.d6, colours.d8, colours.d10, colours.d12, colours.d20];

      for (let i = 0; i < text.length; i += 1) {
        spans += `<span ${i + 1 === text.length ? 'id="last-span"' : ''} style="color:${myColors[i % myColors.length]}; font-weight: bold">${text.charAt(i)}</span>`;
      }
      return spans;
    },
    setCaret() {
      const el = document.getElementById('div-input');
      const range = document.createRange();
      const sel = window.getSelection();
      range.setStart(el.childNodes[this.diceTextInput.length - 1], 1);
      range.collapse(true);
      sel.removeAllRanges();
      sel.addRange(range);
      el.focus();
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.dice-input {
  border: solid;
  border-color: red;
}
</style>
