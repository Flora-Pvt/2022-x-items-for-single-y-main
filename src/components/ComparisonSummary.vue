<script setup>
import { computed } from "vue";
import { useItemComparison } from "../composables/itemComparison";
const { itemsToCompare } = useItemComparison();

const cheapestPrice = computed(() => {
  return Math.min(
    itemsToCompare.value[0]?.price,
    itemsToCompare.value[1]?.price
  );
});

const cheapestItem = computed(() => {
  return itemsToCompare.value.find((i) => i.price === cheapestPrice.value);
});

const expensiveItem = computed(() => {
  return itemsToCompare.value.find((i) => i.price !== cheapestPrice.value);
});

const sameItems = computed(() => {
  return !expensiveItem.value;
});

const computedNumberOfCheapestItem = computed(() => {
  return Math.floor(expensiveItem.value?.price / cheapestItem.value?.price);
});
</script>

<template>
  <p v-if="sameItems" class="mx-5 text-center">Items are the same</p>
  <p v-else class="mx-5 text-center">
    You can get <strong>{{ computedNumberOfCheapestItem }}</strong>
    {{ cheapestItem?.title }} for about the same price as a single
    {{ expensiveItem?.title }}
  </p>
</template>
