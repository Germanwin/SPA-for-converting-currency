<template>
  <div id="app">
    <Header :selectedCurrency="selectedCurrency" @currencySelected="updateCurrency" />
    <router-view :selectedCurrency="selectedCurrency" />
  </div>
</template>

<script>
import { ref } from 'vue';
import Header from '@/components/header.vue';

export default {
  components: {
    Header,
  },
  setup() {
    const selectedCurrency = ref('RUB');

    const updateCurrency = (currency) => {
      selectedCurrency.value = currency;
    };

    return {
      selectedCurrency,
      updateCurrency,
    };
  },
};
</script>