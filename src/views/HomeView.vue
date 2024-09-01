<template>
    <div class="home-view-content">
        <MainCurrency :selectedCurrency="selectedCurrency" />
        <ExchangeRates :selectedCurrency="selectedCurrency" />
    </div>
</template>

<script>
import ExchangeRates from '@/components/exchange-rates.vue';
import MainCurrency from '@/components/main-currency.vue';

export default {
    components: {
        MainCurrency,
        ExchangeRates
    },
    props: {
        selectedCurrency: {
            type: String,
            required: true,
        },
    },
    
};
</script>