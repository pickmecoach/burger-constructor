<template>
  <header class="header">
    <Logo class="header__logo"></Logo>
    <Navigation class="header__navigation"></Navigation>
  </header>
</template>

<script>
  import Logo from './Logo';
  import Navigation from './UI/Navigation';

  export default {
    name: 'Header',
    components: {
      Logo,
      Navigation,
    },
  };
</script>

<style scoped>
  .header {
    height: 56px;
    width: 100%;
    position: fixed;
    top: 0;
    left: 0;
    background-color: #703b09;
    display: -ms-flexbox;
    display: flex;
    -ms-flex-pack: justify;
    justify-content: space-between;
    -ms-flex-align: center;
    align-items: center;
    padding: 0 20px;
    -webkit-box-sizing: border-box;
    box-sizing: border-box;
    z-index: 90
  }

  .header__logo {
    height: 80%
  }

  .header__navigation {
    height: 100%;
  }

</style>
