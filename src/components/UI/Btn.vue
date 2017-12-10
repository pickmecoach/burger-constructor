<template>
  <button class="btn" :data-ingredient="product">
    {{ text }}
  </button>
</template>

<script>
  export default {
    name: 'Btn',
    props: ['text', 'product'],
  };
</script>

<style scoped>
  .btn {
    display: block;
    font: inherit;
    padding: 5px;
    margin: 0 5px;
    width: 80px;
    border: 1px solid #AA6817;
    cursor: pointer;
    outline: none;
    color: #fff;
  }

  .btn:disabled {
    background-color: #AC9980;
    border: 1px solid #7E7365;
    color: #ccc;
    cursor: not-allowed;
  }

  .btn__less {
    background-color: #D39952;
  }

  .btn__more {
    background-color: #8F5E1E;
  }
</style>
