<template>
    <h3>History</h3>
    <ul id="list" class="list">
        <li
            v-for="transaction in transactions"
            :key="transaction.id"
            :class="transaction.amount < 0 ? 'minus' : 'plus'"
        >
            {{ transaction.text }} <span>{{ transaction.amount }}</span>
            <button class="delete-btn">x</button>
        </li>
        <!-- <li class="minus">
            Cash <span>-$400</span><button class="delete-btn">x</button>
        </li>
        <li class="plus">
            Paycheck <span>$400</span><button class="delete-btn">x</button>
        </li> -->
    </ul>
</template>

<script setup lang="ts">
import { defineProps } from "vue";

defineProps({
    transactions: {
        type: Array,
        required: true,
    },
});
</script>
