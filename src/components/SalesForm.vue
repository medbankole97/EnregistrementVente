<template>
  <div class="container mt-5">
    <h2>Enregistrement des ventes</h2>
    <form @submit.prevent="handleSubmit">
      <div class="form-group mb-3">
        <label for="reference">Référence</label>
        <input
          type="text"
          class="form-control"
          id="reference"
          v-model="reference"
          :class="{'is-invalid': errors.reference}"
        />
        <div class="invalid-feedback">{{ errors.reference }}</div>
      </div>

      <div class="form-group mb-3">
        <label for="designation">Désignation</label>
        <input
          type="text"
          class="form-control"
          id="designation"
          v-model="designation"
          :class="{'is-invalid': errors.designation}"
        />
        <div class="invalid-feedback">{{ errors.designation }}</div>
      </div>

      <div class="form-group mb-3">
        <label for="quantity">Quantité vendue</label>
        <input
          type="number"
          class="form-control"
          id="quantity"
          v-model="quantity"
          :class="{'is-invalid': errors.quantity}"
        />
        <div class="invalid-feedback">{{ errors.quantity }}</div>
      </div>

      <div class="form-group mb-3">
        <label for="price">Prix de vente</label>
        <input
          type="number"
          class="form-control"
          id="price"
          v-model="price"
          :class="{'is-invalid': errors.price}"
        />
        <div class="invalid-feedback">{{ errors.price }}</div>
      </div>

      <button type="submit" class="btn btn-primary">Enregistrer</button>
    </form>
  </div>
</template>

<script setup>
import { ref, defineProps } from 'vue';

// Définir les props pour recevoir la fonction du parent
const props = defineProps({
  onSubmit: Function,
});

const reference = ref('');
const designation = ref('');
const quantity = ref('');
const price = ref('');
const errors = ref({});

const validateForm = () => {
  errors.value = {};

  if (!reference.value) {
    errors.value.reference = 'Référence est obligatoire.';
  }
  if (!designation.value) {
    errors.value.designation = 'Désignation est obligatoire.';
  }
  if (!quantity.value || quantity.value <= 0) {
    errors.value.quantity = 'Quantité vendue doit être positive.';
  }
  if (!price.value || price.value <= 0) {
    errors.value.price = 'Prix de vente doit être positif.';
  }

  return Object.keys(errors.value).length === 0;
};

const handleSubmit = () => {
  if (validateForm()) {
    // Appeler la fonction passée via les props pour soumettre les données
    props.onSubmit({
      reference: reference.value,
      designation: designation.value,
      quantity: quantity.value,
      price: price.value,
    });
    resetForm();
  }
};

const resetForm = () => {
  reference.value = '';
  designation.value = '';
  quantity.value = '';
  price.value = '';
};
</script>
