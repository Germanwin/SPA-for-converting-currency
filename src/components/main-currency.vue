<template>
    <div class="main-currency-block">
        <h1>Main currency: </h1>
        <h1 class="main-currency">{{ selectedCurrency }}</h1>
    </div>
</template>

<script>
export default {
    props: {
        selectedCurrency: {
            type: String,
            required: true,
        },
    },
};
</script>
