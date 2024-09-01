<template>
    <div class="converting">
        <div class="converter-form">
            <div class="converter-row">
                <v-select v-model="currencyFrom" :items="currencyOptions" label="From Currency"></v-select>
                <v-text-field v-model.number="amountFrom" label="Amount" type="number" @input="convert"></v-text-field>
            </div>
            <div class="converter-row">
                <v-select v-model="currencyTo" :items="currencyOptions" label="To Currency"></v-select>
                <v-text-field v-model.number="amountTo" label="Amount" type="number" :readonly="true"></v-text-field>
            </div>
        </div>
    </div>
</template>

<script>
import axios from 'axios';

export default {
    data() {
        return {
            currencyFrom: 'RUB',
            currencyTo: 'USD',
            amountFrom: 0,
            amountTo: 0,
            exchangeRates: {},
            currencyOptions: ['RUB', 'USD', 'EUR'],
        };
    },
    methods: {
        async fetchExchangeRates() {
            try {
                const response = await axios.get(
                    'https://status.neuralgeneration.com/api/currency'
                );
                this.exchangeRates = response.data;
                this.convert(); // Convert on data fetch
            } catch (error) {
                console.error('Failed to load exchange rates:', error);
            }
        },
        convert() {
            if (!this.amountFrom) {
                this.amountTo = 0;
                return;
            }

            const rateKey = `${this.currencyFrom.toLowerCase()}-${this.currencyTo.toLowerCase()}`;
            const rate = this.exchangeRates[rateKey];

            if (rate) {
                this.amountTo = (this.amountFrom * rate).toFixed(2);
            } else {
                this.amountTo = 'N/A';
            }
        },
    },
    watch: {
        currencyFrom: 'convert',
        currencyTo: 'convert',
        amountFrom: 'convert',
    },
    mounted() {
        this.fetchExchangeRates();
    },
};
</script>
