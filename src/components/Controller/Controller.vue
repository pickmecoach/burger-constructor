<template>
  <div class="controller">
    <div class="current-price">Current price: {{currentPrice | toCurrency}}</div>
    <div v-for="ingredient in panelOptions" class="controller__row">

      <!-- Опять же почему бы просто не вывести див ? -->
      <div class="controller__label">
        {{ ingredient.name }}
      </div>

      <Btn
        :text="'Less'"
        class="btn__less"
        :disabled="ingredient.quantity === 0"
        :product="ingredient.name"
        @click.native="changeAmount('dec', ingredient.id)"
      ></Btn>
      <Btn
        :text="'More'"
        class="btn__more"
        :product="ingredient.name"
        @click.native="changeAmount('inc', ingredient.id)"
      ></Btn>
    </div>
  </div>
</template>

<script>
  import axios from 'axios';
  import Btn from '../UI/Btn';

  export default {
    name: 'Controller',
    props: {
      panelOptions: {
        type: Array,
        default: () => []
      }
    },
    computed: {

      //- Высчитываем текущую цену
      currentPrice () {
        return this.panelOptions.reduce((acc, next) => {
          return acc += (next.cost * next.quantity)
        }, 0)
      }
    },

    methods: {

      //- Изменяем количество
      changeAmount (type, id) {

        //- Передаем "Наверх" данные об ингридиенте и тип изменения
        this.$emit('update', {type, id})
        //- объект с type и id будет передан в качестве аргумента
        //- в обработчик (см. Бургер)
      },
    },

    //- Фильтры для получения значения со знаками после запятой
    filters: {
      toCurrency (value) {
        return value.toFixed(2)
      }
    },

    components: {
      Btn,
    },
  };
</script>

<style scoped>
 .controller {
   width: 100%;
   margin: auto;
   padding: 10px 0;
   display: flex;
   flex-flow: column;
   align-items: center;

   background-color: #CF8F2E;
   box-shadow: 0 2px 1px #ccc;
 }

  .controller__row {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin: 5px 0;
  }


 .controller__label {
   padding: 10px;
   font-weight: bold;
   width: 80px;
 }
</style>
