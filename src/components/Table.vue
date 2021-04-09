<template>
  <table class="table">
    <thead>
      <tr>
        <th>Label</th>
        <th>Key Words</th>
        <th v-for="col in Object.keys(textColumns)" :key="col">{{ textColumns[col] }}</th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="row in rowData" :key="row.legacy_pk">
        <td>
          <a target="_blank" :href="`https://mmp.acdh-dev.oeaw.ac.at/archiv/stelle/detail/${row.legacy_pk + 1}`">{{
            row["display_label"]
          }}</a>
        </td>
        <td>{{ getKeyWords(row) }}</td>
        <td v-for="col in Object.keys(textColumns)" :key="col">{{ row.text[col] }}</td>
      </tr>
    </tbody>
  </table>
</template>

<script>
export default {
  name: "Table",
  props: { rowData: Array, textColumns: Object },
  methods: {
    getKeyWords(row) {
      return row["key_word"].map((word) => word.stichwort).join(", ");
    },
  },
};
</script>
<style>
.keyword {
  background-color: var(--white);
  border: 2px solid #88dbdf;
  margin: 2px;
  padding: 0 2px;
  border-radius: 3px;
}
.navbar-search-icon {
  border: none;
}
</style>
