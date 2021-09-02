<template>
  <div className="container">
    <button type="button" class="key1">C</button>
    <button type="button" class="key2">+</button>
    <button type="button" class="key3">0</button>
    <button type="button" class="key4">=</button>
    <button
      v-for="(k, i) of [
        '/',
        '*',
        '-',
        '7',
        '8',
        '9',
        '4',
        '5',
        '6',
        '1',
        '2',
        '3',
        '.',
      ]"
      :key="i"
      type="button"
    >
      {{ k }}
    </button>
  </div>
</template>

<script>
export default {
  name: "CalcKeypad",
};
</script>
