<script setup>
import { ref } from 'vue';
import Formulaire from './Formulaire.vue'
import ListeVente from './ListeVente.vue'
const products = ref([
  { reference: '001', designation: 'Laptop', quantite: 10, prix: 999.99 },
  { reference: '002', designation: 'Smartphone', quantite: 25, prix: 499.99 },
  { reference: '003', designation: 'Tablet', quantite: 15, prix: 299.99 },
  { reference: '004', designation: 'Monitor', quantite: 8, prix: 199.99 },
  { reference: '005', designation: 'Keyboard', quantite: 50, prix: 49.99 }
]);
const formComponent = ref();

const add = (reference, designation, quantite, prix) => {
  products.value.push({
    reference,
    designation,
    quantite,
    prix
  });
  console.log("reception evenement");
  
} 

const remove = (index) => {
  products.value.splice(index, 1);
}

const edit = (index) => {
  const product = products.value[index];
  formComponent.value.edit(product);
}


</script>

<template>
     <div class="container">
    <h1 class="text-center border-bottom mb-4">Gestion de Vente</h1>
  
    <Formulaire class="border-bottom pb-4" @on-add="add" ref="formComponent" />

    <ListeVente :products="products" class="mt-4" @on-remove="remove"  @on-edit="edit" />

  </div>
</template>

<style scoped>

</style>
