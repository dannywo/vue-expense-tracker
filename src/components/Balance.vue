<template>
    <h4>Balance</h4>
    <h1 id="balance">${{ total.toFixed(2) }}</h1>
</template>

<script setup lang="ts">
import { defineProps } from "vue";

defineProps({
    total: {
        type: Number,
        required: true,
    },
});
</script>
