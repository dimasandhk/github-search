<template>
  <div class="home mt-5">
    <div class="container">
      <h3 class="text-center mb-3">Search Github User</h3>
      <Form />
    </div>
  </div>
</template>

<script>
import Form from "@/components/Form.vue";

export default {
  name: "Home",
  components: {
    Form,
  },
};
</script>

<style lang="scss">
.home {
  margin-bottom: 100px;
}
</style>
