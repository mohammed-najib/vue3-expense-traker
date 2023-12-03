<template>
  <div class="mb-4">
    <h4 class="text-lg">Your Balance</h4>
    <h1 id="balance" class="font-bold text-2xl">
      {{ `${total < 0 ? "-$" : "$"}` + `${total.toFixed(2)}`.replace("-", "") }}
    </h1>
  </div>
</template>

<script lang="ts" setup>
const props = defineProps<{
  total: number
}>()
</script>
