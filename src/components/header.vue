<script>
import { RouterLink } from 'vue-router'
import HeaderDropdown from './header-dropdown.vue';

export default {
  components: {
    HeaderDropdown,
  },
  props: {
    selectedCurrency: String,
  },
  methods: {
    selectCurrency(currency) {
      this.$emit('currencySelected', currency);
    },
  },
};
</script>

<template>
    <div class="header">
        <RouterLink to="/">Home</RouterLink>
        <RouterLink to="/converting">converting</RouterLink>
        <HeaderDropdown @currencySelected="selectCurrency" />
    </div>
</template>