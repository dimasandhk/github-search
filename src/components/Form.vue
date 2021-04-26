<template>
  <input-container>
    <input
      type="text"
      class="form-control shadow-none"
      placeholder="Github Username"
      v-model="inputValue"
      @keyup="triggerSearch"
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
  </input-container>

  <result-container
    v-for="(data, i) of dataObject"
    :key="i"
    v-show="showResult"
  >
    <div class="col-12 col-md-12 col-lg-6">
      <img :src="data.img" alt="" class="rounded user-image mt-2" />
    </div>
    <div class="col-12 col-md-12 col-lg-6">
      <h5 class="mt-3">{{ data.name }}</h5>
      <h5>@{{ data.username }}</h5>
      <h6 class="mt-3">- Location: {{ data.location }}</h6>
      <h6>- Followers: {{ data.followers }}</h6>
      <h6>- Following: {{ data.following }}</h6>
      <h6>- Public Repos: {{ data.repo }}</h6>
      <h6>- Public Gists: {{ data.gist }}</h6>
      <h6>- Company: {{ data.company }}</h6>
      <h6 class="mt-4">{{ data.email }}</h6>
      <h6>Joined at {{ parseDefaultTime(data.join) }}</h6>
    </div>
    <div class="col-12 col-md-12 col-lg-12">
      <hr />
      <h5 class="text-center">
        {{ data.bio }}
      </h5>
      <hr />
      <h6 class="text-center">Blog: {{ data.blog }}</h6>
      <h6 class="text-center">Twitter: {{ data.twitter }}</h6>
      <hr />
      <Detail :value="inputValue" :data="dataObject[0]" />
      <a
        class="btn btn-block btn-dark shadow-none mt-2"
        target="_blank"
        :href="data.detail"
      >
        Visit Github
      </a>
    </div>
  </result-container>
</template>

<script>
import swal from "sweetalert";
import Container from "./Form/Container.vue";
import InputContainer from "./Form/InputContainer.vue";
import Detail from "./Form/Detail.vue";

export default {
  data: () => ({
    inputValue: "",
    showResult: false,
    dataObject: [],
  }),
  methods: {
    getUserData(username) {
      return fetch(`https://api.github.com/users/${username}`)
        .then((res) => res.json())
        .then((res) => res);
    },
    searchUser: async function() {
      const data = await this.getUserData(this.inputValue);
      if (!this.inputValue) {
        this.showResult = false;
        swal("Error", "The Input is required!", "error");
      } else {
        if (data.type !== "Organization") {
          if (data.message !== "Not Found") {
            this.showResult = true;
            this.assignValue(data);
          } else {
            this.showResult = false;
            swal("Sorry", "User Not Found", "error");
          }
        } else {
          this.inputValue = "";
          this.showResult = false;
          swal("Sorry", "That username is an organization", "error");
        }
      }
    },
    triggerSearch(event) {
      event.keyCode == 13 ? this.searchUser() : undefined;
    },
    assignValue(data) {
      this.dataObject.length >= 1 ? this.dataObject.shift() : undefined;

      this.dataObject.push({
        detail: data.html_url,
        blog: `${!data.blog ? "No Blog" : data.blog}`,
        twitter: `${
          !data.twitter_username ? "No Twitter" : data.twitter_username
        }`,
        img: data.avatar_url,
        name: data.name,
        username: data.login,
        location: `${!data.location ? "No Location" : data.location}`,
        followers: data.followers,
        following: data.following,
        repo: data.public_repos,
        gist: data.public_gists,
        company: `${!data.company ? "No Company" : data.company}`,
        email: `${!data.email ? "No Email" : data.email}`,
        join: this.parseDefaultTime(data.created_at),
        bio: `${!data.bio ? "No Bio" : data.bio}`,
        repoDetail: {
          url: data.repos_url,
        },
      });
    },
    parseDefaultTime: (str) => str.split("T")[0],
  },
  components: {
    "result-container": Container,
    "input-container": InputContainer,
    Detail,
  },
};
</script>

<style lang="scss">
.form-control {
  &:focus {
    border: 2px solid #989a9e;
  }
  color: #000 !important;
}

.swal-modal {
  .swal-icon--info {
    &::before,
    &::after {
      background-color: #a5dc86;
    }
    color: rgba(57, 57, 64, 0.95);
    border: 4px solid #a5dc86;
  }
  .swal-title,
  .swal-text {
    color: #fff;
  }
  .swal-button {
    border: none;
    &:hover {
      color: #fff;
      background-color: #4d4d53 !important;
    }
    background-color: #4d4d53;
    color: #fff;
    font-weight: 600;
  }

  background-color: rgba(57, 57, 64, 0.95);
}
</style>
