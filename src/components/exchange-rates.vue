<template>
    <div class="exchange-rates">
        <div v-if="loading">
            <p>Loading exchange rates...</p>
        </div>
        <div v-else-if="error">
            <p>Error: {{ error }}</p>
        </div>
        <div v-else>
            <div v-if="selectedCurrency === 'RUB'">
                <p>1 USD = {{ formatCurrency(exchangeRates['usd-rub']) }} RUB</p>
                <p>1 EUR = {{ formatCurrency(exchangeRates['eur-rub']) }} RUB</p>
            </div>
            <div v-else-if="selectedCurrency === 'USD'">
                <p>1 RUB = {{ formatCurrency(exchangeRates['rub-usd']) }} USD</p>
                <p>1 EUR = {{ formatCurrency(exchangeRates['eur-usd']) }} USD</p>
            </div>
            <div v-else-if="selectedCurrency === 'EUR'">
                <p>1 RUB = {{ formatCurrency(exchangeRates['rub-eur']) }} EUR</p>
                <p>1 USD = {{ formatCurrency(exchangeRates['usd-eur']) }} EUR</p>
            </div>
        </div>
    </div>
</template>

<script>
import axios from 'axios';

export default {
    props: {
        selectedCurrency: {
            type: String,
            required: true,
        },
    },
    data() {
        return {
            exchangeRates: {},
            loading: false,
            error: null,
        };
    },
    watch: {
        selectedCurrency: 'fetchExchangeRates',
    },
    methods: {
        async fetchExchangeRates() {
            this.loading = true;
            this.error = null;

            try {
                const response = await axios.get(
                    'https://status.neuralgeneration.com/api/currency'
                );

                this.exchangeRates = response.data;

            } catch (err) {
                console.error(err);
                this.error = 'Failed to load exchange rates';
            } finally {
                this.loading = false;
            }
        },
        formatCurrency(value) {
            return value ? value.toFixed(2) : 'N/A'; // Форматируем до двух знаков после запятой
        },
    },
    mounted() {
        this.fetchExchangeRates();
    },
};
</script>

<style scoped>
.exchange-rates p {
    margin: 5px 0;
}
</style>