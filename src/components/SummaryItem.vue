<template>
    <div :class="{ 'bold': featured}" class="summary-item">
        <p>{{ text }}</p>
        <p v-if="isNumber">£{{ amount.toFixed(2) }}</p>
        <p v-else>{{ amount }}</p>
    </div>
</template>


<script>
    export default {

        props: ['text', 'amount', 'featured'],

        computed: {
            isNumber: function() {
                
                if (typeof(this.amount) === 'number') {
                    return true;
                } else return false;
            }
        }
    
    }
</script>


<style scoped>
    .summary-item {
        display: flex;
        justify-content: space-between;
        margin: 0.5em 0;
    }

    .bold {
        font-weight: 700;
    }
</style>