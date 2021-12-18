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
const url1 = "/detection.json";

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
      this.data = res.data;
      var results = res.data;
      var tmplabels = [],tmpdata = [];
      results.forEach(function(x) {
        tmplabels.push(x.date);
        tmpdata.push(parseFloat(x.withhelmet));
      });
      const res1 = await this.$axios.get(url1);
      this.data1 = res1.data1;
      var results1 = res1.data;
      var tmplabels2 = [],tmpdata2 = [];
      results1.forEach(function(y) {
        tmplabels2.push(y.date);
        tmpdata2.push(parseFloat(y.sum));
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
      var tempData2 = {
        labels: tmplabels2,
        datasets: [
          {
            label: "aaa",
            data: tmpdata,
            borderColor: "rgb(255, 0, 0, 2)",
            backgroundColor: "rgba(255, 0, 0, 0.2)",
            borderWidth: 2
          },
        ],
      };
      this.jsonchartdata2 = tempData2;
      this.loaded = true;

    } catch (e) {
      console.error(e);
    }
  },
};
</script>
