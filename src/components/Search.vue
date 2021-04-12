<template>
  <div class="container">
    <!-- Adapted from Fundament -->
    <div class="search-controls">
      <div class="form-inline" role="search" style="grid-area: a">
        <input
          class="form-control navbar-search"
          type="text"
          placeholder="Search for a quote"
          v-model="zitat"
          autocomplete="off"
        />
        <button class="navbar-search-icon" @click="searchButtonClick">
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
      <div class="form-inline" v-if="results.count" style="grid-area: b">
        Results: {{ (page - 1) * limit + 1 }}-{{ Math.min(page * limit, results.count) }}/{{ results.count }}
      </div>
      <div class="paging-controls form-inline" style="grid-area: c">
        Sort by relevance <input class="form-control" type="checkbox" v-model="relevanceSort" />
      </div>
      <div class="paging-controls form-inline" style="grid-area: d">
        Entries per page
        <select class="form-control" v-model="limit">
          <option value="5">5</option>
          <option value="10">10</option>
          <option value="20">20</option>
          <option value="30">30</option>
          <option value="50">50</option>
        </select>
      </div>
      <div class="paging-controls form-inline" style="grid-area: e">
        Go to page
        <select class="form-control" v-model="page">
          <option v-for="i in Math.ceil(results.count / this.limit) || 0" :key="i" :value="i">{{ i }}</option>
        </select>
      </div>
    </div>
    <span v-if="loading">Loading...</span>
    <div class="card">
      <div class="card-body">
        <Table :rowData="sortedRowData" :textColumns="tableCols"></Table>
      </div>
    </div>
  </div>
</template>

<script>
import Table from "./Table.vue";
export default {
  name: "Search",
  components: { Table },
  data() {
    return {
      zitat: "",
      loading: false,
      limit: 20,
      page: 1,
      results: {},
      relevanceSort: false,
      tableCols: { start_date: "From", end_date: "To", author_name: "Author", place_name: "Place" },
    };
  },
  watch: {
    page: function() {
      this.searchZitat();
    },
    limit: function() {
      this.page = 1;
      this.searchZitat();
    },
  },
  computed: {
    sortedRowData() {
      if (this.relevanceSort)
        return this.results.results
          ? this.results.results.slice().sort((a, b) => {
              //compare direct keyword matching
              let direct_keywords_a = a.key_word.filter(
                (keyword) => keyword.stichwort.toLowerCase() == this.zitat.toLowerCase()
              ).length;
              let direct_keywords_b = b.key_word.filter(
                (keyword) => keyword.stichwort.toLowerCase() == this.zitat.toLowerCase()
              ).length;
              if (direct_keywords_a == direct_keywords_b) {
                //compare keyword variant matching
                let keywords_a = a.key_word.filter(
                  (keyword) => keyword.varianten.toLowerCase().indexOf(this.zitat.toLowerCase()) >= 0
                ).length;
                let keywords_b = b.key_word.filter(
                  (keyword) => keyword.varianten.toLowerCase().indexOf(this.zitat.toLowerCase()) >= 0
                ).length;
                if (keywords_a == keywords_b) {
                  let text_matches_a = (a.zitat.toLowerCase().match(this.zitat) || []).length;
                  let text_matches_b = (b.zitat.toLowerCase().match(this.zitat) || []).length;
                  return text_matches_b - text_matches_a;
                } else return keywords_b - keywords_a;
              } else return direct_keywords_b - direct_keywords_a;
            })
          : [];
      else return this.results.results || [];
    },
  },
  methods: {
    searchButtonClick() {
      this.page = 1;
      this.searchZitat();
    },
    searchZitat() {
      const baseUrl = "https://mmp.acdh-dev.oeaw.ac.at/api/stelle/?";
      let params = new URLSearchParams({ zitat: this.zitat, limit: this.limit, offset: (this.page - 1) * this.limit });
      this.loading = true;
      this.results = {};
      fetch(baseUrl + params.toString())
        .then((res) => res.json())
        .then((res) => {
          Promise.all(
            [
              res.results
                .filter((entry) => entry.text.ort.length > 0)
                .map((entry) =>
                  fetch(entry.text.ort[0])
                    .then((placeRes) => placeRes.json())
                    .then((placeRes) => (entry.text.place_name = placeRes.name))
                ),
              res.results
                .filter((entry) => entry.text.autor.length > 0)
                .map((entry) =>
                  fetch(entry.text.autor[0])
                    .then((authorRes) => authorRes.json())
                    .then((authorRes) => (entry.text.author_name = authorRes.name_en))
                ),
            ].flat()
          ).then(() => {
            this.results = res;
            this.loading = false;
          });
        });
    },
  },
};
</script>
<style>
.navbar-search-icon {
  border: none;
  margin-left: 5px;
  background-color: transparent;
}
.search-controls {
  padding: 5px 0;
  display: grid;
  grid-template-areas:
    "a b ."
    "c d e";
  justify-content: space-between;
}
.form-inline {
  display: inline-flex;
}
.paging-controls {
  gap: 5px;
}
.card-body {
  overflow-x: auto;
}
.navbar-search-icon {
  cursor: pointer;
}
@media (min-width: 992px) {
  .search-controls {
    grid-template-areas: "a b c d e";
  }
}
@media (max-width: 576px) {
  .search-controls {
    grid-template-areas:
      "a"
      "b"
      "c"
      "d"
      "e";
  }
  .form-control {
    width: auto;
  }
}
</style>
