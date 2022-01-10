<template>
  <div id="vue" class="counter">
    <button @click="count--">-</button>
    <pre>{{ count }}</pre>
    <button @click="count++">+</button>
  </div>
</template>

<script>
export default {
  data: () => ({
    count: 0,
  }),
  methods: {},
};
</script>
