<template>
  <nav>
    <ul class="navigation">
      <NavigationItem
        :class="{
          'navigation__item': true,
          'active': activeLink === 'home'
        }"
        :where="'home'"
        :text="'Burger Builder'"
      ></NavigationItem>
      <NavigationItem
        :class="{
          'navigation__item': true
        }"
        :where="'checkout'"
        :text="'Checkout'"
      ></NavigationItem>
    </ul>
  </nav>
</template>

<script>
  import NavigationItem from './NavigationItem/NavigationItem';

  export default {
    name: 'Navigation',
    data() {
      return {
        activeLink: 'home',
      };
    },
    components: {
      NavigationItem,
    },
  };
</script>

<style scoped>
  .navigation {
    margin: 0;
    padding: 0;
    list-style: none;
    display: -ms-flexbox;
    display: flex;
    -ms-flex-flow: column;
    flex-flow: column;
    -ms-flex-align: center;
    align-items: center;
    height: 100%
  }

  @media (min-width: 500px) {
    .navigation {
      -ms-flex-flow: row;
      flex-flow: row
    }
  }

  .navigation__item {
    margin: 10px 0;
    -webkit-box-sizing: border-box;
    box-sizing: border-box;
    display: block;
    width: 100%
  }



  @media (min-width: 500px) {
    .navigation__item {
      margin: 0;
      display: -ms-flexbox;
      display: flex;
      height: 100%;
      width: auto;
      -ms-flex-align: center;
      align-items: center
    }
  }
</style>
