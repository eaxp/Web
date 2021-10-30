<template>
  <div>
    <h1>Dashboard</h1>
    <v-row>
      <!--<v-col md="12">
        <v-card>
          <line-chart
            :linechartdata="chartdata"
            :linechartoptions="options"
            :height="300"
          />
        </v-card>
      </v-col>-->
      <br /><br />
      <v-col md="12">
        <v-card v-if="loaded">
          <line-chart
            :linechartdata="jsonchartdata"
            :lineoptions="barchartoptions"
            :height="130"
          />
        </v-card>
      </v-col>
    </v-row>
    
  </div>
</template>

<script>
const url = "/datatest.json";

export default {
  data() {
    return {
      chartdata: {
        labels: ["January", "February", "March", "April"],
        datasets: [
          {
            label: "Data One",
            borderColor: "#f87979",
            data: [40, 20, 50, 10],
            fill: false,
          },
        ],
      },
      options: {
        responsive: true,
        maintainAspectRatio: false,
      },
      loaded: false,
      apichartdata: {
        labels: [],
        datasets: [],
      },
      jsonchartdata: {
        labels: [],
        datasets: [],
      },
      
      data1: null,
      search1: "",
      
      headers1: [
        { text: "ID", align: "start", sortable: true, value: "id" },
        { text: "Sum", value: "sum" },
        { text: "Date", value: "date" },
      ],
    };
  },
  async mounted() {
    this.loaded = false;
    try {
      const res = await this.$axios.get(url);
      var results = res.data;
      var tmplabels = [],
        tmpdata = [];
      results.forEach(function (x) {
        tmplabels.push(x.date);
        tmpdata.push(parseFloat(x.sum));
      });

      var tempData = {
        labels: tmplabels,
        datasets: [
          {
            label: "Sum",
            data: tmpdata,
            borderColor: "rgb(75, 192, 192)",
            backgroundColor: "rgba(75, 192, 192, 0.2)",
          },
        ],
      };
      this.jsonchartdata = tempData;
      this.loaded = true;

      const res1 = await this.$axios.get(url);
        console.log(res1.data1);
        this.data1 = res1.data1;


    } catch (e) {
      console.error(e);
    }
  },
};
</script>
