<template>
    <div class="basket-item">
        <p class="item-name">{{ data.name }}</p>
        <button class="quantity-btn quantity-btn--minus" @click="$emit('remove-item')">-</button>
        <p class="item__quantity">Qty: {{data.quantity}}</p>
        <button class="quantity-btn quantity-btn--plus" @click="$emit('add-item')">+</button>
        <p class="item__totalPrice">£{{ (data.quantity * data.price).toFixed(2) }}</p>
        
    </div>
</template>


<script>
    export default {
        props: ['data']
    }
</script>


<style scoped>
    .basket-item {
        display: flex;
        width: 100%;
        margin: 1em 0;
    }

    .item-name {
        font-weight: 700;
    }

    .quantity-btn {
        width: 25px;
        height: 25px;
        line-height: 25px;
        text-align: center;
        border-radius: 50%;
        border: none;
        background-color: skyblue;
        font-weight: 700;
    }

    .quantity-btn--minus {
        margin-left: auto;
        margin-right: 1em;
    }

    .quantity-btn--plus {
        margin-left: 1em;
        margin-right: 1em;
    }

    .item__totalPrice {
        width: 60px;
        text-align: right;
    }

    @media(max-width: 500px) {
        .basket-item {
            flex-wrap: wrap;
        }
        
        .item-name {
            width: 100%;
            margin: 0 0 0.5rem;
        }

        .quantity-btn--minus {
            margin-left: 0;
        }

        .item__totalPrice {
            margin-left: auto;
        }
    }

</style>