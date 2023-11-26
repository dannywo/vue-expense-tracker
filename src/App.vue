<script setup lang="ts">
import Header from "./components/Header.vue";
import Balance from "./components/Balance.vue";
import IncomeExpenses from "./components/IncomeExpenses.vue";
import TransactionList from "./components/TransactionList.vue";
import AddTransaction from "./components/AddTransaction.vue";

import { ref } from "vue";
import { computed } from "@vue/reactivity";

const transactions = ref([
    { id: 1, text: "Flowers", amount: -19.99 },
    { id: 2, text: "Bi-Weekly Paycheck", amount: 2919.99 },
    { id: 3, text: "Mortgage", amount: -1730.25 },
    { id: 3, text: "Nutflix", amount: -9.99 },
]);

const total = computed(() => {
    return transactions.value.reduce((acc, transaction) => {
        return acc + transaction.amount;
    }, 0);
});

console.log(total.value);
</script>

<template>
    <Header></Header>
    <div class="container">
        <Balance />
        <IncomeExpenses />
        <TransactionList :transactions="transactions" />
        <AddTransaction />
    </div>
</template>
