<template>
  <div class="burger">
    <div class="breadtop">
      <div class="breadtop__seeds_1"></div>
      <div class="breadtop__seeds_2"></div>
    </div>
    <Salad class="burger__ingredient"></Salad>
    <Bacon class="burger__ingredient"></Bacon>
    <Cheese class="burger__ingredient"></Cheese>
    <Cutlet class="burger__ingredient"></Cutlet>
    <div class="breadbottom">
    </div>
  </div>
</template>

<script>
  import axios from 'axios';
  import Cheese from './Cheese';
  import Salad from './Salad';
  import Bacon from './Bacon';
  import Cutlet from './Cutlet';

  const url = 'http://localhost:3000/ingredients';

  export default {
    name: 'Burger',
    data() {
      return {
        ingredients: null,
        error: null,
      };
    },
    created() {
      axios.get(url)
        .then((response) => {
          this.ingredients = response.data;
        })
        .catch((e) => {
          this.error.push(e);
        });
    },
    components: {
      Cheese,
      Salad,
      Bacon,
      Cutlet,
    },
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

  .burger__ingredient {
    margin: 2% auto;
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
