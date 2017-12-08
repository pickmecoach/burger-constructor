<template>
  <div class="logo">
    <img src="/src/img/burger-logo.png" alt="logo burger">
  </div>
</template>

<script>
  export default {
    name: 'Logo',
  };
</script>

<style scoped>
  .logo {
    background-color: #fff;
    padding: 8px;
    -webkit-box-sizing: border-box;
    box-sizing: border-box;
    border-radius: 5px
  }

  .logo img {
    height: 100%
  }
</style>
