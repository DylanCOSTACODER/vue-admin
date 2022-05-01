<template>
  <form>
    <h1 class="h3 mb-3 fw-normal">Please sign in</h1>

    <div class="form-floating">
      <input
        type="email"
        class="form-control"
        id="email"
        placeholder="Email address"
        required
      />
      <label for="email">Email address</label>
    </div>
    <div class="form-floating">
      <input
        type="password"
        class="form-control"
        id="password"
        placeholder="Password"
      />
      <label for="password">Password</label>
    </div>

    <button class="w-100 btn btn-lg btn-primary" type="submit">Sign in</button>
  </form>
</template>

<script lang="ts">
export default {
  name: "Login",
  data() {
    return {};
  },
  methods: {},
};
</script>

<style lang="scss" scoped></style>
