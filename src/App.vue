<template>
  <div className="app light">
    <CalcPanel></CalcPanel>
  </div>
</template>

<script>
import CalcPanel from "./components/CalcPanel.vue";

export default {
  name: "App",
  components: {
    CalcPanel,
  },
};
</script>
