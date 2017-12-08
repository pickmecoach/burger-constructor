<template>
  <div>
    <custom-header/>
    <custom-main/>
  </div>
</template>

<script>
  import Header from './components/Header';
  import Main from './components/Main';

  export default {
    name: 'app',
    components: {
      'custom-header': Header,
      'custom-main': Main,
    },
  };
</script>

<style>

</style>
