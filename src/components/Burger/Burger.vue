<template>
  <!-- Сделаем обертку, чтоб компонент возвращал один элемент -->
  <div class="burger__wrapper">
    <!-- Сам бургер -->
    <div class="burger">
      <div class="breadtop">
        <div class="breadtop__seeds_1"></div>
        <div class="breadtop__seeds_2"></div>
      </div>

      <!-- Не уверен, что для того, чтобы вывести див с определенным классом
      нам нужен отдельный компонент, поэтому как вариант:-->

      <!-- Салат -->
      <div class="burger__ingredients">
        <div class="burger__ingredient salad" v-for="n in getQuantityByName('Salad')"></div>
      </div>

      <!-- Сыр -->
      <div class="burger__ingredients">
        <div class="burger__ingredient cheese" v-for="n in getQuantityByName('Cheese')"></div>
      </div>

      <!-- Бэйкон -->
      <div class="burger__ingredients">
        <div class="burger__ingredient cheese" v-for="n in getQuantityByName('Bacon')"></div>
      </div>

      <!-- Котлетс -->
      <div class="burger__ingredients">
        <div class="burger__ingredient cutlet" v-for="n in getQuantityByName('Cutlet')"></div>
      </div>

      <div class="breadbottom">
      </div>
    </div>

    <!-- "Контрольная панель",
    передаем ей через пропс ингридиенты и вещаем обработчик на кастомное
    событие update, которое и триггерится нами через $emit внутри Controller.
    Назначенный обработчик updateIngredients получит в качестве аргумента то, что
    мы передали в $emit, после названия 'update'-->
    <Controller :panel-options="ingredients" @update="updateIngredients"></Controller>
  </div>
</template>

<script>
  import axios from 'axios';
  import Controller from '../Controller/Controller.vue'
  const url = 'http://localhost:3000/ingredients';

  export default {
    name: 'Burger',
    data() {
      return {
        ingredients: [],
        error: null,
      };
    },
    created() {
      //- Получаем ингридиенты и заносим в стейт ингридиентов
      axios.get(url)
        .then(
          response => { this.ingredients = response.data },
          error => { this.error = error }
        );
    },
    components: {
      Controller: Controller
    },
    computed: {

      //- получаем из массива ингридиентов объект с ключами по id,
      //- удобного поиска
      ingredientsObj () {
        return this.ingredients.reduce((acc, next) => {
          return {...acc, [next.id]: next}
        }, {});
      }
    },
    methods: {
      //- Узнаем количество по названию, раз нам важен порядок
      getQuantityByName (name) {
        return (this.ingredients.find(item => item.name === name) || {}).quantity
      },

      //- обрабатываем инфу с Controller на update
      updateIngredients ({type, id}) {

        //- текущее количество ингридиентов
        let currentValue = this.ingredientsObj[id].quantity

        axios.patch(`${url}/${id}`, {

          //- если тип INC, передаем +1, иначе -1 от текущего
          quantity: type === 'inc' ? currentValue + 1 : currentValue - 1,
        })
        .then(
          res => {
            //- обновляем наш стейт
            this.ingredients = this.ingredients.map(item => {

              //- находим по переданному id, и заменяем на ответ
              if (item.id === id) {
                item = res.data
              }
              return item
            })
          },
          error => null
        )

      }
    }
  };

</script>

<style scoped>
  .burger {
    width: 100%;
    margin: auto;
    height: 250px;
    overflow: scroll;
    text-align: center;
    font-weight: 700;
    font-size: 1.2rem
  }

  .burger__ingredients {
    width: 100%;
  }

  .burger__ingredient {
    margin: 2% auto;
  }

  .burger__ingredient.cheese {
    width: 90%;
    height: 10px;
    background-color: yellow;
  }

  .burger__ingredient.bacon {
    width: 80%;
    height: 10px;
    background-color: hotpink;
  }

  .burger__ingredient.cutlet {
    width: 80%;
    height: 50px;
    border-radius: 10px;
    background-color: brown;
  }

  .burger__ingredient.salad {
    width: 80%;
    height: 10px;
    background-color: greenyellow;
  }

  @media (min-width: 500px) and (min-height: 400px) {
    .burger{
      width: 350px;
      height: 300px
    }
  }

  @media (min-width: 500px) and (min-height: 401px) {
    .burger {
      width: 450px;
      height: 400px
    }
  }

  @media (min-width: 1000px) and (min-height: 700px) {
    .burger {
      width: 700px;
      height: 600px
    }
  }

  .breadbottom {
    height: 13%;
    background: -webkit-gradient(linear, left top, left bottom, from(#f08e4a), to(#e27b36));
    background: -webkit-linear-gradient(#f08e4a, #e27b36);
    background: -o-linear-gradient(#f08e4a, #e27b36);
    background: linear-gradient(#f08e4a, #e27b36);
    border-radius: 0 0 30px 30px
  }

  .breadbottom, .breadtop {
    width: 80%;
    -webkit-box-shadow: inset -15px 0 #c15711;
    box-shadow: inset -15px 0 #c15711;
    margin: 2% auto
  }

  .breadtop {
    height: 20%;
    background: -webkit-gradient(linear, left top, left bottom, from(#bc581e), to(#e27b36));
    background: -webkit-linear-gradient(#bc581e, #e27b36);
    background: -o-linear-gradient(#bc581e, #e27b36);
    background: linear-gradient(#bc581e, #e27b36);
    border-radius: 50% 50% 0 0;
    position: relative
  }

  .breadtop__seeds_1 {
    width: 10%;
    height: 15%;
    position: absolute;
    background-color: #fff;
    left: 30%;
    top: 50%;
    border-radius: 40%;
    -webkit-transform: rotate(-20deg);
    -ms-transform: rotate(-20deg);
    transform: rotate(-20deg);
    -webkit-box-shadow: inset -2px -3px #c9c9c9;
    box-shadow: inset -2px -3px #c9c9c9
  }

  .breadtop__seeds_1:after {
    left: -170%;
    top: -260%;
    -webkit-box-shadow: inset -1px 2px #c9c9c9;
    box-shadow: inset -1px 2px #c9c9c9
  }

  .breadtop__seeds_1:after, .breadtop__seeds_1:before {
    content: "";
    width: 100%;
    height: 100%;
    position: absolute;
    background-color: #fff;
    border-radius: 40%;
    -webkit-transform: rotate(60deg);
    -ms-transform: rotate(60deg);
    transform: rotate(60deg)
  }

  .breadtop__seeds_1:before {
    left: 180%;
    top: -50%;
    -webkit-box-shadow: inset -1px -3px #c9c9c9;
    box-shadow: inset -1px -3px #c9c9c9
  }

  .breadtop__seeds_2 {
    width: 10%;
    height: 15%;
    position: absolute;
    background-color: #fff;
    left: 64%;
    top: 50%;
    border-radius: 40%;
    -webkit-transform: rotate(10deg);
    -ms-transform: rotate(10deg);
    transform: rotate(10deg);
    -webkit-box-shadow: inset -3px 0 #c9c9c9;
    box-shadow: inset -3px 0 #c9c9c9
  }

  .breadtop__seeds_2:before {
    content: "";
    width: 100%;
    height: 100%;
    position: absolute;
    background-color: #fff;
    left: 150%;
    top: -130%;
    border-radius: 40%;
    -webkit-transform: rotate(90deg);
    -ms-transform: rotate(90deg);
    transform: rotate(90deg);
    -webkit-box-shadow: inset 1px 3px #c9c9c9;
    box-shadow: inset 1px 3px #c9c9c9
  }
</style>
