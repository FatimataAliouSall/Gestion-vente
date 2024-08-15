<script setup>
import { computed } from "vue";
const emit = defineEmits(["onRemove", "onEdit"]);

const props = defineProps({
  products: {
    type: Array,
    required: true,
    default: [],
  },
});

const total = computed(() =>
  props.products.reduce((acc, item) => acc + item.prix * item.quantite, 0)
);

const destroy = (index) => {
  emit("onRemove", index);
};
const edit = (index) => {
  emit("onEdit", index);
};
</script>

<template>
  <div>
    <table class="table table-bordered table-sm">
      <thead>
        <tr>
          <th scope="col">#</th>
          <th scope="col">Référence</th>
          <th scope="col">Désignation</th>
          <th scope="col">Quantité</th>
          <th scope="col">Prix</th>
          <th scope="col">Montant</th>
          <th scope="col">Action</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(product, index) in products" :key="index">
          <td>{{ index + 1 }}</td>
          <td>{{ product.reference }}</td>
          <td>{{ product.designation }}</td>
          <td>{{ product.quantite }}</td>
          <td>{{ product.prix }}</td>
          <td>{{ product.quantite * product.prix }}</td>
          <td>
            <button class="btn btn-xs btn-danger" @click="destroy(index)">
              -
            </button>
            <button class="btn btn-xs btn-secondary" @click="edit(index)">
              -
            </button>
          </td>
        </tr>
      </tbody>
      <tfoot>
        <tr>
          <td colspan="5" class="text-center">Total</td>
          <td>{{ total }}</td>
        </tr>
      </tfoot>
    </table>
  </div>
</template>

<style scoped>
</style>
