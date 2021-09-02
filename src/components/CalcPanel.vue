<template>
  <span class="panel">
    <CalcOutput></CalcOutput>
    <CalcKeypad></CalcKeypad>
  </span>
</template>

<script>
import CalcOutput from "./CalcOutput.vue";
import CalcKeypad from "./CalcKeypad.vue";

export default {
  name: "Panel",
  components: {
    CalcOutput,
    CalcKeypad,
  },
};
</script>
