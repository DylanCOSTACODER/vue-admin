<template>
  <h2>Products</h2>
  <div class="d-flex justify-content-end pb-2">
    <router-link
      to="/products/create"
      class="btn btn-dark d-flex align-content-center"
      ><i class="material-icons">&#xE147;</i>
      <span>Add New Product</span>
    </router-link>
  </div>

  <div class="table-responsive">
    <table class="table table-striped table-dark">
      <thead>
        <tr>
          <th>#</th>
          <th>Image</th>
          <th>Title</th>
          <th>Description</th>
          <th>Price</th>
          <th>Action</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="product in products" :key="product.id">
          <td>{{ product.id }}</td>
          <td><img :src="product.image" height="50" /></td>
          <td>{{ product.title }}</td>
          <td>{{ product.description }}</td>
          <td>{{ product.price }}</td>
          <td>
            <router-link :to="`/products/${product.id}/edit`" class="edit"
              ><i class="material-icons">&#xE254;</i></router-link
            >
            <a href="#" class="delete" @click="del(product.id)"
              ><i class="material-icons">&#xE872;</i></a
            >
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script lang="ts">
import { ref, onMounted } from "vue";
import axios from "axios";
import { Entity } from "@/interfaces/entity";
export default {
  name: "Products",
  setup() {
    const products = ref([]);

    onMounted(async () => {
      const response = await axios.get(`products`);
      products.value = response.data.data;
    });

    const del = async (id: number) => {
      if (confirm("Are you sure you want to delete this record?")) {
        await axios.delete(`products/${id}`);
        products.value = products.value.filter((e: Entity) => e.id !== id);
      }
    };
    return {
      products,
      del,
    };
  },
};
</script>
