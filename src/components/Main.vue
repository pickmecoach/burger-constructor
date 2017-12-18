<template>
  <main class="main">
    <Burger></Burger>
  </main>
</template>

<script>
  import Burger from './Burger/Burger';
  import Controller from './Controller/Controller';

  export default {
    name: 'Main',
    components: {
      Burger,
    },
  };
</script>

<style scoped>
  .main {
    margin-top: 72px;
  }
</style>
