<template>
  <div class="flex flex-col mt-8">
    <h3 class="font-bold">History</h3>
    <div class="h-[1px] my-1 bg-gray-500 opacity-[0.25]"></div>
    <ul>
      <li
        v-for="transaction in transactions"
        :key="transaction.id"
        @click="
          itemIdHoverOn === transaction.id
            ? (itemIdHoverOn = null)
            : (itemIdHoverOn = transaction.id)
        "
        :class="
          transaction.amount < 0
            ? 'flex my-2 p-2 bg-white shadow border-r-4 border-red-600'
            : 'flex my-2 p-2 bg-white shadow border-r-4 border-green-600'
        "
        @mouseenter="itemIdHoverOn = transaction.id"
        @mouseleave="itemIdHoverOn = null"
      >
        <div class="relative w-full flex">
          {{ transaction.text }}
          <span class="ml-auto">{{
            `${transaction.amount < 0 ? "-$" : "$"}` +
            `${transaction.amount.toFixed(2)}`.replace("-", "")
          }}</span>
          <button
            @click="deleteTransaction(transaction.id)"
            :class="
              itemIdHoverOn === transaction.id
                ? 'absolute top-0 -left-8 px-2 bg-red-500 rounded-sm text-white block'
                : 'absolute top-0 -left-8 px-2 bg-red-500 rounded-sm text-white hidden'
            "
          >
            x
          </button>
        </div>
      </li>
    </ul>
  </div>
</template>

<script lang="ts" setup>
import { ref } from "vue"

type Transaction = {
  id: number
  text: string
  amount: number
}

const props = defineProps<{
  transactions: Transaction[]
}>()

var itemIdHoverOn = ref<number | null>(null)

const emit = defineEmits(["transactionDeleted"])

const deleteTransaction = (id: number) => {
  emit("transactionDeleted", id)
}
</script>
