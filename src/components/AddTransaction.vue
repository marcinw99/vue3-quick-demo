<template>
  <h3>Add new transaction</h3>
  <form id="form" @submit.prevent="onSubmit">
    <div class="form-control">
      <label for="text">Text</label>
      <input type="text" id="text" v-model="text" placeholder="Enter text..." />
    </div>
    <div class="form-control">
      <label for="amount"
        >Amount <br />
        (negative - expense, positive - income)</label
      >
      <input type="number" id="amount" v-model="amount" placeholder="Enter amount..." />
    </div>
    <button class="btn">Add transaction</button>
  </form>
</template>

<script setup lang="ts">
import { ref } from 'vue'

const text = ref<string>('')
const amount = ref<number>(0)

const emit = defineEmits(['transactionSubmitted'])

const onSubmit = () => {
  if (!text.value || !amount.value || amount.value === 0) {
    return
  }

  const transactionData = {
    text: text.value,
    amount: amount.value
  }

  emit('transactionSubmitted', transactionData)

  text.value = ''
  amount.value = 0
}
</script>
