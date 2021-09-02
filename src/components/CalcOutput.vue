<template>
  <div
    class="output"
    v-bind:class="{ smaller: text.length >= 10, smallest: text.length >= 20 }"
  >
    {{ text }}
  </div>
</template>

<script>
export default {
  name: "CalcOutput",
  props: {
    text: { type: String },
  },
};
</script>
