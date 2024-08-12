<script setup>
import { reactive } from 'vue';

const props = defineProps({
  onSubmit: Function,
});

const nouvelleVente = reactive({
  reference: '',
  designation: '',
  quantite: null,
  prix: null,
});

const erreurs = reactive({
  reference: false,
  designation: false,
  quantite: false,
  prix: false,
});

const enregistrerVente = () => {
  resetErreurs();

  if (validerVente()) {
    props.onSubmit({ ...nouvelleVente });
    resetForm();
  }
};

const validerVente = () => {
  let valide = true;

  if (!nouvelleVente.reference) {
    erreurs.reference = true;
    valide = false;
  }
  if (!nouvelleVente.designation) {
    erreurs.designation = true;
    valide = false;
  }
  if (nouvelleVente.quantite <= 0) {
    erreurs.quantite = true;
    valide = false;
  }
  if (nouvelleVente.prix <= 0) {
    erreurs.prix = true;
    valide = false;
  }

  return valide;
};

const resetErreurs = () => {
  erreurs.reference = false;
  erreurs.designation = false;
  erreurs.quantite = false;
  erreurs.prix = false;
};

const resetForm = () => {
  nouvelleVente.reference = '';
  nouvelleVente.designation = '';
  nouvelleVente.quantite = null;
  nouvelleVente.prix = null;
};
</script>
<template>
    <form @submit.prevent="enregistrerVente">
      <div class="mb-3">
        <label for="reference" class="form-label">Référence du produit</label>
        <input
          type="text"
          id="reference"
          v-model="nouvelleVente.reference"
          class="form-control"
          :class="{'is-invalid': erreurs.reference}"
        />
        <div class="invalid-feedback">Référence est requise.</div>
      </div>
  
      <div class="mb-3">
        <label for="designation" class="form-label">Désignation</label>
        <input
          type="text"
          id="designation"
          v-model="nouvelleVente.designation"
          class="form-control"
          :class="{'is-invalid': erreurs.designation}"
        />
        <div class="invalid-feedback">Désignation est requise.</div>
      </div>
  
      <div class="mb-3">
        <label for="quantite" class="form-label">Quantité vendue</label>
        <input
          type="number"
          id="quantite"
          v-model="nouvelleVente.quantite"
          class="form-control"
          :class="{'is-invalid': erreurs.quantite}"
        />
        <div class="invalid-feedback">Quantité doit être un nombre positif.</div>
      </div>
  
      <div class="mb-3">
        <label for="prix" class="form-label">Prix de vente</label>
        <input
          type="number"
          id="prix"
          v-model="nouvelleVente.prix"
          class="form-control"
          :class="{'is-invalid': erreurs.prix}"
        />
        <div class="invalid-feedback">Prix doit être un nombre positif.</div>
      </div>
  
      <button type="submit" class="btn btn-primary">Enregistrer la vente</button>
    </form>
  </template>
  
<style scoped>

</style>
