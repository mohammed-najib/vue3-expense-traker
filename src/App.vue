<script setup lang="ts"></script>

<template>
  <div
    class="h-screen p-8 flex flex-col items-center justify-center bg-[#f7f7f7]"
  >
    <div class="h-full max-w-[300px] w-full flex flex-col">
      <Header />
      <div class="mb-8">
        <Balance :total="total" />
        <IncomeExpenses :income="income" :expense="expense" />
        <TransactionsList
          :transactions="transactions"
          @transactionDeleted="handleTransactionDeleted"
        />
        <AddTransaction @transactionSubmitted="handleTransactionSubmitted" />
      </div>
      <Footer />
    </div>
  </div>
</template>

<script lang="ts" setup>
import { ref, computed, onMounted } from "vue"
import { useToast } from "vue-toastification"

import Header from "./components/Header.component.vue"
import Balance from "./components/Balance.component.vue"
import IncomeExpenses from "./components/IncomeExpenses.component.vue"
import TransactionsList from "./components/TransactionsList.component.vue"
import AddTransaction from "./components/AddTransaction.component.vue"
import Footer from "./components/Footer.component.vue"

const toast = useToast()

const transactions = ref([])

onMounted(() => {
  const savedTransactions = localStorage.getItem("transactions")

  if (savedTransactions) {
    transactions.value = JSON.parse(savedTransactions)
  }
})

const total = computed(() => {
  return transactions.value.reduce((acc, item) => (acc += item.amount), 0)
})

const income = computed(() => {
  return transactions.value
    .filter((item) => item.amount > 0)
    .reduce((acc, item) => (acc += item.amount), 0)
})

const expense = computed(() => {
  return transactions.value
    .filter((item) => item.amount < 0)
    .reduce((acc, item) => (acc += item.amount), 0)
})

const handleTransactionSubmitted = (transactionData: {
  text: string
  amount: number
}) => {
  if (!text.value || !amount.value) {
    toast.error("Both Text and Amount are required fields")
    return
  }

  const newId = generateUniqueId()
  if (transactions.value.find((item) => item.id === newId)) {
    handleTransactionSubmitted(transactionData)
    return
  }

  transactions.value.push({
    id: newId,
    ...transactionData,
  })

  saveTransactionsToLocalStorage()

  toast.success("Transaction added successfully")
}

const generateUniqueId = () => {
  return Math.floor(Math.random() * 100000000)
}

const handleTransactionDeleted = (id) => {
  transactions.value = transactions.value.filter((item) => item.id !== id)

  saveTransactionsToLocalStorage()

  toast.success("Transaction deleted successfully")
}

const saveTransactionsToLocalStorage = () => {
  localStorage.setItem("transactions", JSON.stringify(transactions.value))
}
</script>
