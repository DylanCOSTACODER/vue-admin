<template>
  <h2>Users</h2>
  <div class="d-flex justify-content-end pb-2">
    <router-link
      to="/users/create"
      class="btn btn-dark d-flex align-content-center"
      ><i class="material-icons">&#xE147;</i>
      <span>Add New Employee</span>
    </router-link>
  </div>
  <div class="table-responsive">
    <table class="table table-striped table-dark">
      <thead>
        <tr>
          <th scope="col">#</th>
          <th scope="col">Name</th>
          <th scope="col">Email</th>
          <th scope="col">Role</th>
          <th scope="col">Action</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="user in users" :key="user.id">
          <td>{{ user.id }}</td>
          <td>{{ user.first_name }} {{ user.last_name }}</td>
          <td>{{ user.email }}</td>
          <td>{{ user.role.name }}</td>
          <td>
            <router-link :to="`/users/${user.id}/edit`" class="edit"
              ><i class="material-icons">&#xE254;</i></router-link
            >
            <a href="#" class="delete" @click="del(user.id)"
              ><i class="material-icons">&#xE872;</i></a
            >
          </td>
        </tr>
      </tbody>
    </table>
  </div>
  <nav aria-label="...">
    <ul class="pagination">
      <li class="page-item">
        <a class="page-link" href="#" @click="previous">Previous</a>
      </li>
      <li class="page-item">
        <a class="page-link" href="#" @click="next">Next</a>
      </li>
    </ul>
  </nav>
</template>

<script lang="ts">
import { ref, onMounted } from "vue";
import axios from "axios";
import { Entity } from "@/interfaces/entity";
export default {
  name: "Users",
  setup() {
    const users = ref([]);
    const page = ref(1);
    const lastPage = ref(0);

    const load = async () => {
      const response = await axios.get(`users?page=${page.value}`);

      users.value = response.data.data;
      lastPage.value = response.data.meta.last_page;
    };

    const next = async () => {
      if (page.value === lastPage.value) return;
      page.value++;
      await load();
    };

    const previous = async () => {
      if (page.value === 1) return;
      page.value--;
      await load();
    };

    const del = async (id: number) => {
      if (confirm("Are you sure you want to delete this record ?")) {
        await axios.delete(`users/${id}`);

        users.value = users.value.filter((e: Entity) => e.id !== id);
      }
    };

    onMounted(load);

    return {
      users,
      next,
      previous,
      del,
      load,
    };
  },
  methods: {},
};
</script>
<style>
.edit {
  color: yellow;
}

.delete {
  color: red;
}
</style>

function load(load: any) { throw new Error('Function not implemented.'); }
