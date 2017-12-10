<template>
  <li>
    <router-link :to="where" class="navigation__link">
      {{ text }}
    </router-link>
  </li>
</template>

<script>
  export default {
    name: 'NavigationItem',
    props: ['text', 'where'],
  };
</script>

<style scoped>
  .navigation__link {
    width: 100%;
    color: #8f5c2c;
    text-decoration: none;
    -webkit-box-sizing: border-box;
    box-sizing: border-box;
    display: block;
    cursor: pointer;
  }

  .router-link-active,
  .navigation__link:active,
  .navigation__link:hover {
    color: #40a4c8
  }

  @media (min-width: 500px) {

    .navigation__link {
      color: #fff;
      height: 100%;
      padding: 16px 10px;
      border-bottom: 4px solid transparent
    }

    .router-link-active,
    .navigation__link:active,
    .navigation__link:hover {
      background-color: #8f5c2c;
      border-bottom: 4px solid #40a4c8;
      color: #fff
    }
  }
</style>
