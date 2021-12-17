<template>
  <div>
    <v-row>
      <v-col cols="1"></v-col>
      <v-col cols="11"><h1>Dashboard</h1></v-col>
    </v-row>
    <v-row>
      <v-col md="12">
        <v-card v-if="loaded">        
          <bar-chart
            :barchartdata="jsonchartdata"
            :barchartoptions="barchartoptions"
            :height="600"/>
        </v-card>
      </v-col>
    </v-row>
    
  </div>
</template>

<script>
const url = "/aaa20.json";

export default {
  data() {
    return { 
      data1: null,
      search1: "",   
      headers1: [
        { text: "ID", align: "start", sortable: true, value: "id" },
        { text: "Sum", value: "sum" },
        { text: "Date", value: "date" },
      ],
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
            borderColor: "rgb(255, 179, 0, 2)",
            backgroundColor: "rgba(255, 179, 0, 0.2)",
            borderWidth: 2
          },
        ],
      };
      this.jsonchartdata = tempData;
      this.loaded = true;

    } catch (e) {
      console.error(e);
    }
  },
};
</script>
