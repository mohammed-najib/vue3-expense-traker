<template>
  <div class="flex flex-col mt-8">
    <h3 class="font-bold">Add new transaction</h3>
    <div class="h-[1px] my-1 bg-gray-500 opacity-[0.25]"></div>
    <form id="form" @submit.prevent="onSubmit">
      <div class="flex flex-col my-2 p-2">
        <label for="text" class="font-bold text-sm">Text</label>
        <input
          type="text"
          id="text"
          v-model="text"
          placeholder="Enter text..."
          class="p-2"
        />
      </div>
      <div class="flex flex-col my-2 p-2">
        <label for="amount" class="font-bold text-sm">
          Amount <br />
          (negative - expense, positive - income)
        </label>
        <input
          type="number"
          id="amount"
          v-model="amount"
          placeholder="Enter amount..."
          class="p-2"
        />
      </div>
      <button class="w-full p-2 bg-purple-600 hover:bg-purple-500 text-white">
        Add transaction
      </button>
    </form>
  </div>
</template>

<script lang="ts" setup>
import { ref } from "vue"

const text = ref("")
const amount = ref("")

const emit = defineEmits(["transactionSubmitted"])

const onSubmit = () => {
  const transactionData = {
    text: text.value,
    amount: parseFloat(amount.value),
  }

  emit("transactionSubmitted", transactionData)

  text.value = ""
  amount.value = ""
}
</script>
