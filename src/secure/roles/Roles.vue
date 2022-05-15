<template>
  <h2>Roles</h2>
  <div class="d-flex justify-content-end pb-2">
    <router-link
      to="/roles/create"
      class="btn btn-dark d-flex align-content-center"
      ><i class="material-icons">&#xE147;</i>
      <span>Add New Role</span>
    </router-link>
  </div>
  <div class="table-responsive">
    <table class="table table-striped table-dark">
      <thead>
        <tr>
          <th scope="col">#</th>
          <th scope="col">Name</th>
          <th scope="col">Action</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="role in roles" :key="role.id">
          <td>{{ role.id }}</td>
          <td>{{ role.name }}</td>
          <td>
            <router-link :to="`/roles/${role.id}/edit`" class="edit"
              ><i class="material-icons">&#xE254;</i></router-link
            >
            <a href="#" class="delete" @click="del(role.id)"
              ><i class="material-icons">&#xE872;</i></a
            >
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script lang="ts">
import axios from "axios";
import { ref, onMounted } from "vue";
import { Entity } from "@/interfaces/entity";
export default {
  name: "Roles",
  setup() {
    const roles = ref([]);

    onMounted(async () => {
      const response = await axios.get("roles");

      roles.value = response.data.data;
    });

    const del = async (id: number) => {
      if (confirm("Are you sure you want to delete this record?")) {
        await axios.delete(`roles/${id}`);
        roles.value = roles.value.filter((e: Entity) => e.id !== id);
      }
    };

    return {
      roles,
      del,
    };
  },
};
</script>

<style lang="scss" scoped></style>
