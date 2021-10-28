<template>
    <div>
        <h1>page show data tables</h1><br><br><br>
        <!--<h2 v-if="data">{{data[0].id}}</h2>-->
        
        <v-card>
            <v-card-title>
                Data table
                    <v-spacer></v-spacer>
                        <v-text-field v-model="search" append-icon="mdi-magnify" label="Search"
                        single-lin hide-details >
                        </v-text-field>
            </v-card-title>
            <v-data-table :headers="headers" :items="data" :search="search" v-if="data">
            </v-data-table>
            <br><br>
        </v-card><br><br><br>
    </div>
</template>
<script>
const url = "/datatest.json";

export default {
    data(){
        return{
            data: null,
            search: "",
            headers: [
                { text: "ID", align: "start", sortable: true, value: "id" },
                { text: "Sum", value: "sum"},
                { text: "Date", value: "date" },                
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