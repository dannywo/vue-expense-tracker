<template>
    <h3></h3>
    <form id="form" @submit.prevent="onSubmit">
        <div class="form-control">
            <label for="text">Text</label>
            <input
                type="text"
                id="text"
                v-model="text"
                placeholder="Enter text..."
            />
        </div>
        <div class="form-control">
            <label for="amount"
                >Amount<br />
                (negative - expense, positive - income)</label
            >
            <input
                type="text"
                id="amount"
                v-model="amount"
                placeholder="Enter amount..."
            />
        </div>
        <button class="btn">Add transaction</button>
    </form>
</template>

<script setup lang="ts">
import { ref } from "vue";

const text = ref("");
const amount = ref("");

const onSubmit = () => {
    console.log("submitted.");
    console.log(text.value);
    console.log(amount.value);
};
</script>
