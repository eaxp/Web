<template>
  <div>
    <h1>Dashboard</h1>
    <v-row>
      <v-col md="12">
        <v-card v-if="loaded">
          <line-chart
            :linechartdata="jsonchartdata"
            :lineoptions="barchartoptions"
            :height="200"/>
        </v-card>
      </v-col>
      <!--<v-col md="6">
        <v-card v-if="loaded">
          <line-chart
            :linechartdata="jsonchartdata"
            :lineoptions="barchartoptions"
            :height="200"/>
        </v-card>
      </v-col>-->
    </v-row>
    
  </div>
</template>

<script>
const url = "/aaa20.json";

export default {
  data() {
    return { 
     barchartoptions: {
        responsive: true,
        maintainAspectRatio: false,
        scales: {
          yAxes: [
            {
              ticks: {
                beginAtZero: true
              }
            }
          ]
        }
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
            label: "Person",
            data: tmpdata,
            borderColor: "rgb(240, 98, 146)",
            backgroundColor: "rgba(240, 98, 146, 0.2)",
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
