<template>
    <div>
        <h>page show data tables</h>
        <h2 v-if="data">{{data[0].id}}</h2>
        
        <v-card>
            <v-card-title>
        Employee table
        <v-spacer></v-spacer>
        <v-text-field
          v-model="search"
          append-icon="mdi-magnify"
          label="Search"
          single-lin
          hide-details
        >
        </v-text-field>
      </v-card-title>
      <v-data-table
        :headers="headers"
        :items="data"
        :search="search"
        v-if="data">
        </v-data-table>
<br><br>


        
      
        </v-card>
    </div>
</template>
<script>
const url = "/data.json";
export default {
    data(){
        return{
            data: null,
            search: "",
            headers: [
                { text: "ID", align: "start", sortable: true, value: "id" },
                { text: "T/F", value: "t/f" },
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
  methods: {
      getColor (calories) {
        if (calories > 400) return 'red'
        else if (calories > 200) return 'orange'
        else return 'green'
      },
    },
}
</script>