<template>
    <div>
        <h1>page show data tables</h1><br><br><br>
        <!--<h2 v-if="data">{{data[0].id}}</h2>-->
        
        <v-card>
            <v-card-title>
                Data table
                    <v-spacer></v-spacer>
                        <v-text-field v-model="search" append-icon="mdi-magnify" label="Search"
                        single-lin hide-details>
                        </v-text-field>
            </v-card-title>
            <v-data-table :headers="headers" :items="data" :search="search" v-if="data">
            </v-data-table>
            <br><br>
        </v-card><br><br><br>
        <!--<v-card>
            <v-card-title>
                Data table 01
                    <v-spacer></v-spacer>
                        <v-text-field v-model="search" append-icon="mdi-magnify" label="Search"
                        single-lin hide-details>
                        </v-text-field>
            </v-card-title>
            <v-data-table :headers="headers1" :items="data1" :search="search1" v-if="data1">
            </v-data-table>
        </v-card>-->
    </div>
</template>
<script>
const url = "/datatest.json";
const url1 ="/data.json";
export default {
    data(){
        return{
            data: null,
            data1: null,
            search1: "",
            search: "",
            headers: [
                { text: "ID", align: "start", sortable: true, value: "id" },
                { text: "Sum", value: "sum"},
                { text: "Date", value: "date" },                
            ],
            headers1: [
                { text: "ID", align: "start", sortable: true, value: "id" },
                { text: "T/F", value: "t/f"},
                { text: "Date", value: "time" },                
            ],
        }
    },
    async mounted() {
    try {
        const res = await this.$axios.get(url);
        console.log(res.data);
        this.data = res.data;

    }
    catch (e) {
        console.error(e);
    }
  },
}
</script>