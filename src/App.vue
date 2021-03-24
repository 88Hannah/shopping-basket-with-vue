<template>
  <div id="app">
    <h1>The Colour Shop</h1>
    <product v-for="(item, index) in products" :key="index" :data="item" @add-product="addProduct(item.itemId)"></product>
    <basket :products="products"></basket>
  </div>
</template>

<script>

  import Product from './components/Product';
  import Basket from './components/Basket';

  import blue from './assets/images/blue.jpg'
  import green from './assets/images/green.jpg'
  import orange from './assets/images/orange.jpg'
  import pink from './assets/images/pink.jpg'
  import purple from './assets/images/purple.jpg'
  import red from './assets/images/red.jpg'
  import yellow from './assets/images/yellow.jpg'

  export default {
    name: 'App',
    
    components: {
      Product,
      Basket
    }, 

    data: function () {
      return {
        publicPath: process.env.BASE_URL,

        products: [
          {
            name: 'Blue Board',
            price: 5.79,
            image: blue,
            itemId: 1
          }, 
          {
            name: 'Green Garden',
            price: 8.35,
            image: green,
            itemId: 2
          },
          {
            name: 'Orange Orange',
            price: 4.50,
            image: orange,
            itemId: 3
          },
          {
            name: 'Pink Pinapple',
            price: 7.29,
            image: pink,
            itemId: 4
          },
          {
            name: 'Purple Petals',
            price: 6.85,
            image: purple,
            itemId: 5
          },
          {
            name: 'Red Robes',
            price: 9.50,
            image: red,
            itemId: 6
          },
          {
            name: 'Yummy Yellow',
            price: 3.89,
            image: yellow,
            itemId: 7
          }
        ]
      }
    },



  }
</script>

<style>
  *,
  *::before,
  *::after {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
    }
  

  body {
    font-family: 'Roboto', sans-serif;
  }

  #app {
    width: 90%;
    max-width: 600px;
    margin: 3em auto;
  }

  img {
    max-width: 100%;
    display: block;
  }

  button {
    cursor: pointer;
  }

</style>
