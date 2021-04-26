<template>
  <nav class="navbar navbar-expand-lg navbar-dark">
    <div class="container text-center">
      <router-link class="navbar-brand mx-auto" to="/"
        ><Logo class="svg"
      /></router-link>
    </div>
  </nav>
</template>

<script>
import Logo from "./Navbar/Logo.vue";

export default {
  components: {
    Logo,
  },
};
</script>

<style lang="scss" scoped>
.navbar {
  .svg {
    width: 32px;
    height: 32px;
  }
  .nav-link {
    &:hover {
      color: #989a9e !important;
    }
    font-weight: 500;
    color: #fff !important;
  }
  .navbar-brand {
    font-weight: 600;
  }
  background-color: #161b22;
}
</style>
