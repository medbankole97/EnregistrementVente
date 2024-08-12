<template>
  <div>
    <SalesForm :onSubmit="addSale" />
    <SalesList :sales="sales" />
  </div>
</template>

<script setup>
import { ref } from 'vue';
import SalesForm from './components/SalesForm.vue';
import SalesList from './components/SalesList.vue';

const sales = ref([]);

const addSale = (sale) => {
  sales.value.push(sale);
};
</script>
