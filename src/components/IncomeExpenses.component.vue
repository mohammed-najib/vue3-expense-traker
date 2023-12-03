<template>
  <div class="flex bg-white shadow">
    <div class="flex-1 flex flex-col p-4 items-center">
      <h4>Income</h4>
      <p class="text-green-600">+${{ income.toFixed(2) }}</p>
    </div>
    <div class="w-[1px] my-4 bg-gray-500 opacity-[0.25]"></div>
    <div class="flex-1 flex flex-col p-4 items-center">
      <h4>Expense</h4>
      <p class="text-red-600">
        -${{ `${expense.toFixed(2)}`.replace("-", "") }}
      </p>
    </div>
  </div>
</template>

<script lang="ts" setup>
const props = defineProps<{
  income: number
  expense: number
}>()
</script>
