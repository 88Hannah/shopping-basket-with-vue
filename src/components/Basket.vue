<template>
    <div>
        <basket-item 
        v-for="item in basketProducts" 
        :key="item.name" 
        :data="item" 
        @add-item="addProduct(item.itemId)" 
        @remove-item="removeProduct(item.itemId)"
        ></basket-item>
        <summary-item text="Sub-total" :amount="subTotal"></summary-item>
        <summary-item text="Shipping" :amount="shipping"></summary-item>
        <summary-item text="Total" :amount="total" :featured="true"></summary-item>
        <p v-if="untilFreeShipping > 0" class="shipping-message shipping-message__cost">Spend another £{{ untilFreeShipping.toFixed(2) }} to get free shipping</p>
        <p v-else class="shipping-message shipping-message__free">You have qualified for free shipping</p>
    </div>
</template>


<script>
    import BasketItem from './BasketItem';
    import SummaryItem from './SummaryItem';

    import EventBus from '../bus';
    
    export default {
        components: {
            BasketItem,
            SummaryItem
        }, 

        props: ['products'],

        data: function () {
            EventBus.$on('add-product', (id) => {
                    this.addProduct(id);
            });

            return {

                basketProducts: []

            }
            
        },
        
        methods: {          

            addProduct: function (id) {
                let basketIndex = this.basketProducts.findIndex(item => item.itemId === id);

                if (basketIndex >= 0) {
                    this.basketProducts[basketIndex].quantity ++;
                } else {
                    let newItem = this.products[this.products.findIndex(item => item.itemId === id)];
                    this.basketProducts.push({ ...newItem, quantity: 1})
                }

            }, 

            removeProduct: function (id) {
                let basketIndex = this.basketProducts.findIndex(item => item.itemId === id);

                if(this.basketProducts[basketIndex].quantity === 1) {
                    this.basketProducts.splice(basketIndex, 1);
                } else if(this.basketProducts[basketIndex].quantity > 1) {
                    this.basketProducts[basketIndex].quantity --;
                }
            }           
  
        },

        computed: {

            subTotal: function () {
                const getSubTotal = (sum, item) => {
                    return sum + (item.price * item.quantity);
                }
                return (this.basketProducts.reduce(getSubTotal, 0));
            },

            total: function () {
                if (typeof(shipping) === 'number') {
                    return (this.subTotal + this.shipping);
                } else return this.subTotal;
            },

            shipping: function () {
                if (this.subTotal === 0) {
                    return 0;
                } else if (this.subTotal < 50) {
                    return 4.99;
                } else {
                    return 'Free';
                }
            }, 

            untilFreeShipping: function () {
                let difference = 50 - this.subTotal;
                if (difference > 0) {
                    return difference;
                } else return 0;
            }
    
        }
    }
</script>


<style scoped>
    .shipping-message {
        text-align: right;
    }

    .shipping-message__cost {
        color: red;
    }

    .shipping-message__free {
        color: green;
    }
</style>