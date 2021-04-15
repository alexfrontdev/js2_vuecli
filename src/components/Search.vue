<template>
  <input
    @input="$emit('searched-text', $event.target.value)"
    placeholder="введите название товара.."
  />
</template>
<script>
export default {
  data: () => ({}),
};
</script>
<style></style>
