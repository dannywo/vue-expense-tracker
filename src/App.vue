<template>
    <Header></Header>
    <div class="container">
        <Balance :total="+total" />
        <IncomeExpenses :income="+income" :expense="+expense" />
        <TransactionList
            :transactions="transactions"
            @transactionDeleted="handleTransactionDeleted"
        />
        <AddTransaction @transactionSubmitted="handleTransactionSubmitted" />
    </div>
</template>

<script setup lang="ts">
import Header from "./components/Header.vue";
import Balance from "./components/Balance.vue";
import IncomeExpenses from "./components/IncomeExpenses.vue";
import TransactionList from "./components/TransactionList.vue";
import AddTransaction from "./components/AddTransaction.vue";

import { useToast } from "vue-toastification";

import { ref, computed, onMounted } from "vue";

const toast = useToast();

type Transaction = [
    {
        id: Number;
        text: String;
        amount: number;
    }
];

const transactions = ref<Transaction[]>([]);

onMounted(() => {
    const savedTransactions = JSON.parse(
        localStorage.getItem("transactions") || "[{}]"
    );
    console.log(savedTransactions);
    if (savedTransactions) {
        transactions.value = savedTransactions;
    }
});

//Get total balance
const total = computed(() => {
    return transactions.value.reduce((acc, transaction) => {
        return acc + transaction.amount;
    }, 0);
});

//Get income
const income = computed(() => {
    return transactions.value
        .filter((tran) => {
            return tran.amount > 0;
        })
        .reduce((acc, transaction) => {
            return acc + transaction.amount;
        }, 0)
        .toFixed(2);
});

//Get expenses
const expense = computed(() => {
    return transactions.value
        .filter((tran) => {
            return tran.amount < 0;
        })
        .reduce((acc, transaction) => {
            return acc + transaction.amount;
        }, 0)
        .toFixed(2);
});

//Add transaction
const handleTransactionSubmitted = (transaction) => {
    console.log(transaction);
    console.log(transactions.value);
    transactions.value.push({
        id: generateId(),
        text: transaction.text,
        amount: transaction.amount,
    });

    saveTransactionsToLocalStorage();

    toast.success("Added successfully");
    console.log(generateId());
};

//Delete transaction
const handleTransactionDeleted = (id) => {
    transactions.value = transactions.value.filter((transaction) => {
        return transaction.id !== id;
    });

    saveTransactionsToLocalStorage();

    toast.success("Deleted successfully");
};

//generate unigue id
const generateId = (): Number => {
    return Math.floor(Math.random() * 10000000);
};

//save to localStorage
const saveTransactionsToLocalStorage = () => {
    localStorage.setItem("transactions", JSON.stringify(transactions.value));
};
</script>
