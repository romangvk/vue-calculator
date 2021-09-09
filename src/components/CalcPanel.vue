<template>
  <span class="panel">
    <CalcOutput :text="text"></CalcOutput>
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
        case "(":
          // don't put an open paren after a decimal point
          if (!/\.$/.test(prev)) this.text = prev + "(";
          break;
        case ")":
          // only put a close paren if there is an open paren that has not been closed
          if (
            /(\d|\))$/.test(prev) &&
            (prev.match(/\(/g) || []).length > (prev.match(/\)/g) || []).length
          )
            this.text = prev + ")";
          break;
        case "↩":
          this.text = this.text = prev.replace(/.$/, "");
          break;
        case "^":
        case "/":
        case "*":
        case "+":
          // only add an operator after a number or close paren
          if (/(\d|\))$/.test(prev)) this.text = prev + key;
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
          if (!/\.\d*$/.test(prev)) this.text = prev + ".";
          break;
        case "=":
          // evaluate if the expression ends in a number or a close paren
          // and also that the number of close parens matches the number of open parens
          if (
            /(\d|\))$/.test(prev) &&
            (prev.match(/\(/g) || []).length ===
              (prev.match(/\)/g) || []).length
          )
            this.text = String(evaluate(prev)).replace(/e\+?/, "*10^");
          break;
        default:
          this.text = prev + key;
      }
    },
  },
};
</script>
