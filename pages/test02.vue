<template>
  <div>
    <h1>Dashboard</h1>
    <v-row>
        <v-col md="6">
            <v-card v-if="loaded">
                <line-chart
                    :linechartdata="jsonchartdata"
                    :lineoptions="barchartoptions"
                    :height="300"/>
            </v-card>
        </v-col>
        <v-col md="6">
            <v-card v-if="loaded1">
                <line-chart
                    :linechartdata="jsonchartdata1"
                    :lineoptions="barchartoptions"
                    :height="300"/>
            </v-card>
        </v-col>
    </v-row>
  </div>
</template>

<script>
const url = "/aaaaa copy 2.json";

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
        datasets: []
      },
      loaded1: false,
      jsonchartdata1: {
        labels1: [],
        datasets1: []
      },
    };
  },
  async mounted(){
      this.loaded = false;
      this.loaded1 = false;
      try {
        const res = await this.$axios.get(url);
        var results = res.data;
        var tmplabels = [],tmpdata = [];
        results.forEach(function(x) {
          tmplabels.push(x.date);
          tmpdata.push(parseFloat(x.sum));
        });
        var tempData = {
          labels: tmplabels,
          datasets: [
            {
              label: "sum by date",
              data: tmpdata,
              borderColor: "rgb(75, 192, 192)",
              backgroundColor: "rgba(75, 192, 192, 0.2)"
            }
          ]
        };
        this.jsonchartdata = tempData;

       

        this.loaded = true;
        this.loaded1 = true;
      } catch (e) {
        console.error(e);
      }
  }
};
</script>
