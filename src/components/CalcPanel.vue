<template>
  <span class="panel">
    <CalcOutput text="text"></CalcOutput>
    <CalcKeypad @keypress="keypress"></CalcKeypad>
  </span>
</template>

<script>
import CalcOutput from "./CalcOutput.vue";
import CalcKeypad from "./CalcKeypad.vue";

import evaluate from "../lib/evaluate";

export default {
  name: "CalcPanel",
  components: {
    CalcOutput,
    CalcKeypad,
  },
  data: function() {
    {
      return { text: "" };
    }
  },
  methods: {
    keypress: function(key) {
      let prev = this.text;
      if (
        this.text === "NaN" ||
        this.text === "Infinity" ||
        this.text === "-Infinity" ||
        this.text === "Err: Division by 0"
      ) {
        prev = "";
      }
      switch (key) {
        case "C":
          this.text = "";
          break;
        case "/":
        case "*":
        case "+":
          // only add an operator after a number
          if (/\d$/.test(prev)) this.text = prev + key;
          break;
        case "-":
          // preceded by + change to minus
          if (/\+$/.test(prev)) this.text = prev.replace(/.$/, "-");
          // preceded by - change to plus
          else if (/\d-$/.test(prev)) this.text = prev.replace(/.$/, "+");
          // preceded by - but that is the whole string
          else if (/^-$/.test(prev)) this.text = prev.replace(/.$/, "");
          else this.text = prev + "-";
          break;
        case ".":
          // don't put two decimal points in a row
          if (!/\.$/.test(prev)) this.text = prev + key;
          break;
        case "=":
          if (/^.*\d+$/.test(prev)) {
            this.text = String(evaluate(prev));
          }
          break;
        default:
          this.text = prev + key;
      }
    },
  },
};
</script>
