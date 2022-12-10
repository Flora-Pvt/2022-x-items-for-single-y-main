<script setup>
import ItemSelect from "./components/ItemSelect.vue";
import ComparisonSummary from "./components/ComparisonSummary.vue";
import { useItemComparison } from "./composables/itemComparison";
const { availableItems, itemsToCompare } = useItemComparison();

const getProducts = () => {
  fetch("https://dummyjson.com/products")
    .then((res) => res.json())
    .then((data) => {
      availableItems.value = data.products;
    })
    .catch(() => alert("An error occured"));
};

getProducts();
</script>

<template>
  <div class="w-full h-full flex flex-col gap-5 justify-center items-center">
    <h1 class="text-4xl font-bold">Select items to compare</h1>
    <div class="flex flex-col gap-5 justify-center">
      <ItemSelect />
      <ItemSelect />
    </div>
    <ComparisonSummary v-if="itemsToCompare.length === 2" />
  </div>
</template>
