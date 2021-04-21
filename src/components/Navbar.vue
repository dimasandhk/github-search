<template>
  <nav class="navbar navbar-expand-lg navbar-dark">
    <div class="container">
      <router-link class="navbar-brand" to="/"><Logo class="svg"/></router-link>
      <navbar-toggler />
      <div class="collapse navbar-collapse" id="navbarNavAltMarkup">
        <div class="navbar-nav ml-auto">
          <router-link class="nav-link mr-3" to="/">Home</router-link>
          <a class="nav-link" href="#">About</a>
        </div>
      </div>
    </div>
  </nav>
</template>

<script>
import Button from "./Navbar/Button.vue";
import Logo from "./Navbar/Logo.vue";

export default {
  components: {
    "navbar-toggler": Button,
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
