<template>
  <div class="container mt-5">
    <h3>Ventes enregistrées</h3>
    <table class="table table-bordered">
      <thead>
        <tr>
          <th>Référence</th>
          <th>Désignation</th>
          <th>Quantité vendue</th>
          <th>Prix de vente</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(sale, index) in sales" :key="index">
          <td>{{ sale.reference }}</td>
          <td>{{ sale.designation }}</td>
          <td>{{ sale.quantity }}</td>
          <td>{{ sale.price }}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script setup>
import { defineProps } from 'vue';

const props = defineProps({
  sales: {
    type: Array,
    required: true,
  },
});
</script>
