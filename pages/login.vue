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

const url = "/aaaaa.json"

export default {
    data(){
        return{
            data1: null,
            
            search: "",
           
            headers: [
                { text: "Date", align: "start", sortable: true, value: "date" },
                { text: "With Helmat", value: "with helmat"},
                { text: "Without Helmat", value: "without helmat" }, 
                { text: "Sum (With/Without Helmat)", value: "sum"}               
            ],
        }
    },
    async mounted() {
    try {
        const res1 = await this.$axios.get(url);
        console.log(res1.data1);
        this.data1 = res1.data1;

    }
    catch (e) {
        console.error(e);
    }
  },
}
</script>