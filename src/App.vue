<template>
  <Header />
  <div class="container">
    <Balance :total="total" />
    <IncomeExpenses :income="total_income" :expenses="total_expenses" />
    <TransactionList :transactions="transactions" />
    <AddTransaction />
  </div>
</template>

<script setup lang="ts">
import { computed, ref } from 'vue'

import Header from './components/Header.vue'
import Balance from './components/Balance.vue'
import IncomeExpenses from './components/IncomeExpenses.vue'
import TransactionList from '@/components/TransactionList.vue'
import AddTransaction from '@/components/AddTransaction.vue'

const transactions = ref([
  { id: 1, text: 'Flower', amount: -20 },
  { id: 2, text: 'Salary', amount: 300 },
  { id: 3, text: 'Book', amount: -10 },
  { id: 4, text: 'Camera', amount: 150 }
])

const total_income = computed(() => {
  return transactions.value.reduce((acc, transaction) => {
    if (transaction.amount > 0) {
      return acc + transaction.amount
    }
    return acc
  }, 0)
})
const total_expenses = computed(() => {
  return transactions.value.reduce((acc, transaction) => {
    if (transaction.amount < 0) {
      return acc - transaction.amount
    }
    return acc
  }, 0)
})

const total = computed(() => total_income.value - total_expenses.value)
</script>
