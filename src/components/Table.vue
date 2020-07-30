<template>
  <table id="thirdTable">
    <thead>
      <tr>
        <th v-for="(col, index) in columns" :key="index">{{ col }}</th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="(row, index) in rows" :key="index">
        <template v-for="(value, name) in rows[index]">
          <td v-if="name === 'imgSource'" :key="value">
            <img :src="value" alt="Avatar" />
          </td>
          <td v-else :key="value">{{value}}</td>
        </template>
      </tr>
    </tbody>
  </table>
</template>

<script>
export default {
  name: "DataTable",
  props: {
    rows: { type: Array },
    columns: { type: Array },

    // columns: ["Name", "Age", "Avatar"]
  },
  methods: {
    sortTable: function sortTable(col) {
      this.rows.sort(function (a, b) {
        if (a[col] > b[col]) {
          return 1;
        } else if (a[col] < b[col]) {
          return -1;
        }
        return 0;
      });
    },
  },
  // computed: {
  //     "columns": function columns() {
  //         if (this.rows.length === 0) {
  //             return [];
  //         }
  //         console.log(Object.keys(this.rows[0]));
  //         return Object.keys(this.rows[0])
  //     }
  // }
};
</script>

<style lang="scss">
table {
  font-family: "Open Sans", sans-serif;
  border-collapse: collapse;
  border: 3px solid #44475c;
  margin: 10px 10px 0 10px;
  th {
    text-transform: uppercase;
    text-align: left;
    background: #44475c;
    color: #fff;
    cursor: pointer;
    padding: 8px;
    min-width: 30px;
  }
  th:hover {
    background: #717699;
  }
  td {
    text-align: left;
    padding: 8px;
    border-right: 2px solid #7d82a8;
  }
  td:last-child {
    border-right: none;
  }
  tbody tr:nth-child(2n) td {
    background: #d4d8f9;
  }
 
    img {
        max-width: 180px;
    }
}

</style>