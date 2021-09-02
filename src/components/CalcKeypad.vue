<template>
  <div className="container">
    <button type="button" class="key1" v-on:click="$emit('keypress', 'C')">
      C
    </button>
    <button type="button" class="key2" v-on:click="$emit('keypress', '+')">
      +
    </button>
    <button type="button" class="key3" v-on:click="$emit('keypress', '0')">
      0
    </button>
    <button type="button" class="key4" v-on:click="$emit('keypress', '=')">
      =
    </button>
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
      v-on:click="$emit('keypress', k)"
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
