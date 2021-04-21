<template>
  <div class="row justify-content-center mt-3">
    <div class="col-12 col-md-12 col-lg-8">
      <div class="input-group mb-3">
        <input
          type="text"
          class="form-control shadow-none"
          placeholder="Github Username"
          v-model="inputValue"
        />
        <div class="input-group-append">
          <button
            class="btn btn-dark shadow-none"
            @click="searchUser"
            type="button"
          >
            Search
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      inputValue: "",
    };
  },
  methods: {
    getUserData(username) {
      return fetch(`https://api.github.com/users/${username}`)
        .then((res) => res.json())
        .then((res) => res);
    },
    searchUser: async function() {
      const data = await this.getUserData(this.inputValue);
      console.log(data);
    },
  },
};
</script>

<style lang="scss" scoped>
.form-control {
  &:focus {
    border: 2px solid #989a9e;
  }
  color: #000 !important;
}
</style>
