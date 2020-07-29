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
                    <img :src="value" alt="Avatar">
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
        rows: {type: Array},
        columns: {type: Array}

        // columns: ["Name", "Age", "Avatar"]
    },
    // data: () => {
    //     return {
    //         rows: [
    //             {name: "Chandler Bing", age: 23, imgSource: 'https://placeholder.com/100'},
    //             {name: "Ross Geller", age: 19, imgSource: 'https://placeholder.com/100'},
    //             {name: "Rachel Green", age: 23, imgSource: 'https://placeholder.com/100'},
    //             {name: "Monica Geller", age: 24, imgSource: 'https://placeholder.com/100'},
    //             {name: "Joey Tribbiani", age: 26, imgSource: 'https://placeholder.com/100'},
    //             {name: "Phoebe Buffay", age: 27, imgSource: 'https://placeholder.com/100'}
    //         ],
    //         columns: ["Name", "Age", "Avatar"]
    //     }
    // },
    methods: {
        "sortTable": function sortTable(col) {
            this.rows.sort(function (a, b) {
                if (a[col] > b[col]) {
                    return 1;
                } else if (a[col] < b[col]) {
                    return -1;
                }
                return 0;
            })
        }
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
}

</script>

<style>
table {
    font-family: 'Open Sans', sans-serif;
    width: 750px;
    border-collapse: collapse;
    border: 3px solid #44475C;
    margin: 10px 10px 0 10px;
}

table th {
    text-transform: uppercase;
    text-align: left;
    background: #44475C;
    color: #FFF;
    cursor: pointer;
    padding: 8px;
    min-width: 30px;
}
table th:hover {
    background: #717699;
}
table td {
    text-align: left;
    padding: 8px;
    border-right: 2px solid #7D82A8;
}
table td:last-child {
    border-right: none;
}
table tbody tr:nth-child(2n) td {
    background: #D4D8F9;
}

table {
    font-family: 'Open Sans', sans-serif;
    width: 750px;
    border-collapse: collapse;
    border: 3px solid #44475C;
    margin: 10px 10px 0 10px;
}

table th {
    text-transform: uppercase;
    text-align: left;
    background: #44475C;
    color: #FFF;
    cursor: pointer;
    padding: 8px;
    min-width: 30px;
}
table th:hover {
    background: #717699;
}
table td {
    text-align: left;
    padding: 8px;
    border-right: 2px solid #7D82A8;
}
table td:last-child {
    border-right: none;
}
table tbody tr:nth-child(2n) td {
    background: #D4D8F9;
}
</style>