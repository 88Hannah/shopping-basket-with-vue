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

            }
            
        },
        
        methods: {          
            addProduct: function (id) {
                this.products[this.products.findIndex(item => item.itemId === id)].quantity ++;
            }, 

            removeProduct: function (id) {
                if(this.products[this.products.findIndex(item => item.itemId === id)].quantity > 0) {
                this.products[this.products.findIndex(item => item.itemId === id)].quantity --;
                }
            }           
  
        },

        computed: {
            basketProducts: function () {
                return this.products.filter(item => item.quantity > 0);
            }, 

            subTotal: function () {
                const getSubTotal = (sum, item) => {
                    return sum + (item.price * item.quantity);
                }
                return (this.products.reduce(getSubTotal, 0));
            },

            total: function () {
                return (this.subTotal + this.shipping);
            },

            shipping: function () {
                if (this.subTotal > 0) {
                    return 4.99;
                } else {
                    return 0;
                }
            }
    
        }
    }
</script>


<style scoped>

</style>