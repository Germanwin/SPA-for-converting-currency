<template>
    <v-menu>
        <template v-slot:activator="{ props }">
            <v-btn color="rgb(1, 201, 97)" dark v-bind="props">
                Main Currency
            </v-btn>
        </template>

        <v-list>
            <v-list-item v-for="(item, index) in items" :key="index" @click="selectCurrency(item.title)">
                <v-list-item-title>{{ item.title }}</v-list-item-title>
            </v-list-item>
        </v-list>
    </v-menu>
</template>

<script>
export default {
    data: () => ({
        items: [
            { title: 'RUB' },
            { title: 'USD' },
            { title: 'EUR' },
        ],
    }),
    methods: {
        selectCurrency(currency) {
            this.$emit('currencySelected', currency);
        },
    },
};
</script>