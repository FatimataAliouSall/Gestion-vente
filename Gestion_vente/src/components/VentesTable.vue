<template>
    <table class="table table-striped">
      <thead>
        <tr>
          <th>Référence</th>
          <th>Désignation</th>
          <th>Quantité</th>
          <th>Prix</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="vente in ventes" :key="vente.reference">
          <td>{{ vente.reference }}</td>
          <td>{{ vente.designation }}</td>
          <td>{{ vente.quantite }}</td>
          <td>{{ vente.prix }}</td>
        </tr>
      </tbody>
    </table>
  </template>
  
  <script setup>
  const props = defineProps({
    ventes: Array,
  });
  </script>
  