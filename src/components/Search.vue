<template>
  <div>
    <!-- Adapted from Fundament -->
    <div class="form-inline my-2 my-lg-0 navbar-search-form" method="get" action="/" role="search">
      <input class="form-control navbar-search" type="text" placeholder="Search" v-model="zitat" autocomplete="off" />
      <button class="navbar-search-icon" @click="searchZitat">
        <svg
          xmlns="http://www.w3.org/2000/svg"
          width="24"
          height="24"
          viewBox="0 0 24 24"
          fill="none"
          stroke="currentColor"
          stroke-width="2"
          stroke-linecap="round"
          stroke-linejoin="round"
          class="feather feather-search"
        >
          <circle cx="11" cy="11" r="8"></circle>
          <line x1="21" y1="21" x2="16.65" y2="16.65"></line>
        </svg>
      </button>
    </div>
    <span v-if="loading">Loading...</span>
    <div v-for="result in results.results" :key="result.legacy_pk">
      <a :href="`https://mmp.acdh-dev.oeaw.ac.at/archiv/stelle/detail/${result.legacy_pk + 1}`" target="blank">{{
        result.display_label
      }}</a>
      <span v-for="keyWord in result.key_word" :key="keyWord.legacy_pk">
        {{ keyWord.stichwort }}
      </span>
    </div>
  </div>
</template>

<script>
export default {
  name: "Search",
  data() {
    return {
      zitat: "",
      loading: false,
      results: {},
    };
  },
  computed: {},
  methods: {
    searchZitat() {
      const baseUrl = "https://mmp.acdh-dev.oeaw.ac.at/api/stelle/?";
      let params = new URLSearchParams({ zitat: this.zitat, limit: 20 });
      this.loading = true;
      this.results = {};
      fetch(baseUrl + params)
        .then((res) => res.json())
        .then((res) => {
          this.results = res;
          this.loading = false;
        });
    },
  },
};
</script>
