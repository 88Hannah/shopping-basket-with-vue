<template>
    <div :class="{ 'bold': featured}" class="summary-item">
        <p>{{ text }}</p>
        <p>£{{ amount.toFixed(2) }}</p>
    </div>
</template>


<script>
    export default {

        props: ['text', 'amount', 'featured']
    
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