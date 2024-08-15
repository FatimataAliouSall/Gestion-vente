<script setup>
import { ref, defineExpose  } from "vue";
const emit = defineEmits(["onAdd"]);

const reference = ref("");
const designation = ref("");
const quantite = ref(1);
const prix = ref(0);
const onSubmit = () => {
  emit("onAdd", reference.value, designation.value, quantite.value, prix.value);

  reference.value = "";
  designation.value = "";
  quantite.value = "";
  prix.value = "";
};
const edit = (product) => {
  reference.value = product.reference;
  designation.value = product.designation;
  quantite.value = product.quantite;
  prix.value = product.prix;
};

defineExpose({
  edit,
});
</script>

<template>
  <div class="container">
    <form class="row gx-3 gy-2 align-items-center" @submit.prevent="onSubmit">
      <div class="col-sm-3">
        <label for="reference">Référence</label>
        <input
          type="text"
          class="form-control"
          id="reference"
          v-model="reference"
        />
      </div>
      <div class="col-sm-3">
        <label for="designation">Désignation</label>
        <input
          type="text"
          class="form-control"
          id="designation"
          v-model="designation"
        />
      </div>
      <div class="col-sm-2">
        <label for="quantite">Quantité</label>
        <input
          type="number"
          class="form-control"
          id="quantite"
          v-model.number="quantite"
        />
      </div>
      <div class="col-sm-2">
        <label for="prix">Prix</label>
        <input
          type="number"
          class="form-control"
          id="prix"
          v-model.number="prix"
        />
      </div>

      <div class="col-auto">
        <button type="submit" class="btn btn-sm mt-4 btn-primary">
          Enregistrer
        </button>
      </div>
    </form>
  </div>
</template>

<style scoped>
</style>
