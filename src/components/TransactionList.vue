<template>
  <h3>History</h3>
  <ul id="list" class="list">
    <li
      v-for="transaction in transactions"
      :key="transaction.id"
      :class="transaction.amount < 0 ? 'minus' : 'plus'"
    >
      {{ transaction.text }} <span>${{ transaction.amount }}</span>
      <button class="delete-btn">x</button>
    </li>
  </ul>
</template>

<script setup lang="ts">
interface Transaction {
  id: number
  amount: number
  text: string
}

const props = defineProps<{
  transactions: Transaction[]
}>()
</script>
