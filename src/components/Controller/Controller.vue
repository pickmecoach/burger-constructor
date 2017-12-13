<template>
  <div class="controller">
    <div class="current-price">Current price: {{currentPrice}}</div>
    <div v-for="ingredient in ingredients" class="controller__row">
      <ControllerLabel
        :text="ingredient.name"
      ></ControllerLabel>
      <Btn
        :text="'Less'"
        class="btn__less"
        :disabled= true
        :product="ingredient.name"
        @click.native="SubtractIngredient(ingredient.id)"
      ></Btn>
      <Btn
        :text="'More'"
        class="btn__more"
        :product="ingredient.name"
        @click.native="AddIngredient(ingredient.id, counter)"
      ></Btn>
    </div>
  </div>
</template>

<script>
  import axios from 'axios';
  import Btn from '../UI/Btn';
  import ControllerLabel from './ControllerLabel/ControllerLabel';

  const url = 'http://localhost:3000/ingredients/';

  export default {
    name: 'Controller',
    props: {
      price: {
        type: Number,
        default: 4.00,
      },
    },
    data() {
      return {
        currentPrice: this.price.toFixed(2),
        ingredients: null,
        error: null,
        counter: 0,
      };
    },
    created() {
      axios.get(url)
        .then((response) => {
          this.ingredients = response.data;
        })
        .catch((e) => {
          this.errors.push(e);
        });
    },
    methods: {
      AddIngredient(ingredient, counter) {
        let urlCurrent = url;
        let counterCurrent = counter;
        counterCurrent += 1;
        urlCurrent += ingredient;
        axios.patch(urlCurrent, {
          quantity: counterCurrent,
        })
        .then(() => {})
        .catch((e) => {
          this.errors.push(e);
        });
      },
    },
    components: {
      Btn,
      ControllerLabel,
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
