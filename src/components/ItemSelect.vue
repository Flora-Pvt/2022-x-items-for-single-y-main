<script setup>
import { ref, watch } from "vue";
import { useItemComparison } from "../composables/itemComparison";

const { availableItems, itemsToCompare } = useItemComparison();

const selected = ref({});

watch(selected, (newItem, prevItem) => {
  itemsToCompare.value = itemsToCompare.value.filter(
    (item) => item.id !== prevItem?.id
  );
  itemsToCompare.value.push(newItem);
});
</script>

<template>
  <select v-model="selected" class="p-2 border-2 border-gray-dark">
    <option disabled value="">Select an item</option>
    <option v-for="product in availableItems" :value="product">
      {{ product.title }} - ${{ product.price }}
    </option>
  </select>
</template>
