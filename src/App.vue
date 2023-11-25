<script setup lang="ts">
import Header from "./components/Header.vue";
import Balance from "./components/Balance.vue";
import IncomeExpenses from "./components/IncomeExpenses.vue";
</script>

<template>
    <Header></Header>
    <div class="container">
        <Balance />
        <IncomeExpenses />
    </div>
</template>
