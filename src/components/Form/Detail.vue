<template>
  <button
    class="btn btn-block btn-dark shadow-none mt-3"
    data-toggle="modal"
    data-target="#repoDetail"
    @click="showData"
  >
    View Repositories
  </button>
  <!-- Modal -->
  <div class="modal fade" id="repoDetail" aria-hidden="true">
    <div class="modal-dialog modal-lg modal-dialog-scrollable">
      <div class="modal-content">
        <div class="modal-header">
          <h5 class="modal-title">{{ data.username }}'s Repositories</h5>
          <close-button></close-button>
        </div>
        <div class="modal-body">
          <div class="row justify-content-center">
            <div
              class="col-12 col-md-12 col-lg-12"
              v-for="({ name, desc, url, lang }, i) in dataApi"
              :key="i"
            >
              <div class="result res-modal mt-2 rounded">
                <h5>{{ name }}</h5>
                <p>Desc: {{ desc || "No Desc" }}</p>
                <p class="p-terakhir">Lang: {{ lang || "No Lang" }}</p>
                <a
                  class="btn btn-block shadow-none btn-dark"
                  :href="url"
                  target="_blank"
                >
                  Detail
                </a>
              </div>
            </div>
          </div>
        </div>
        <div class="modal-footer">
          <button
            type="button"
            class="btn btn-outline-light shadow-none"
            data-dismiss="modal"
          >
            Close
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Button from "./CloseButton.vue";

export default {
  data() {
    return {
      dataApi: [],
    };
  },
  props: {
    value: {
      type: String,
      required: true,
    },
    data: {
      type: Object,
      required: true,
    },
  },
  methods: {
    getReposDetail() {
      return fetch(`https://api.github.com/users/${this.value}/repos`)
        .then((res) => res.json())
        .then((res) => res);
    },
    showData: async function() {
      const data = await this.getReposDetail();
      this.dataApi.length >= 1 ? (this.dataApi = []) : undefined;

      data.forEach((repo) => {
        this.dataApi.push({
          name: repo.name,
          desc: repo.description,
          url: repo.html_url,
          lang: repo.language,
        });
      });
    },
  },
  components: {
    "close-button": Button,
  },
};
</script>

<style lang="scss" scoped>
.modal-content {
  background-color: #343a40;
}

.res-modal {
  .p-terakhir {
    margin-top: -12px;
  }
}
</style>
