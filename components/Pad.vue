<template>
  <div
    class="pad"
    @click="$emit('triggered', sourceUrl)">
  </div>
</template>

<script>
  export default {
    props: {
      sourceUrl: String
    }
  }
</script>

<style>
  .pad {
    margin: 10px;
    width: 40px;
    height: 40px;
    background-color: #000;
    cursor: pointer;
  }
</style>
