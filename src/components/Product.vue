<template>
    <div class="product-container">
        <img :src="data.image" alt="" class="product__img">
        <h2 class="product__name">{{ data.name }}</h2>
        <p class="product__price">£{{ data.price.toFixed(2) }}</p>
        <button class="product__add" @click="addProduct">Add</button>
    </div>
</template>


<script>
    import EventBus from '../bus';

    export default {
        props: ['data'], 

        methods: {
            addProduct: function () {
                console.log("Hello, someone clicked me!");
                EventBus.$emit('add-product', this.data.itemId);
            }
        }

    }
</script>


<style scoped>

    .product-container {
        margin: 2em 0;
        display: flex;
        width: 100%;
        align-items: center;
    }

    .product__name {
        font-size: 1.3em;
        margin-left: 0.5rem;
    }

    .product__img {
        width: 80px;
    }

    .product__price {
        margin-left: auto;
        margin-right: 2em;
    }

    .product__add {
        padding: 0.5em 1em;
        background-color: skyblue;
        border: none;
        border-radius: 10px;
    }

    @media(max-width: 500px) {
        .product-container {
            flex-wrap: wrap;
        }
        
        .product__name {
            order: -1;
            width: 100%;
            margin: 0 0 0.3rem;
        }
    }

</style>