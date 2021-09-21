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
      <br><br>
      <v-col md="12">
        <v-card v-if="loaded">
          <line-chart
            :linechartdata="jsonchartdata"
            :lineoptions="barchartoptions"
            :height="300"
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
            fill: false
          }
        ]
      },
      options: {
        responsive: true,
        maintainAspectRatio: false
      },
      loaded: false,
      apichartdata: {
        labels: [],
        datasets: []
      },
      jsonchartdata: {
        labels: [],
        datasets: []
      },
    };
  },
  async mounted(){
      this.loaded = false;
      try {
        const res = await this.$axios.get(url);
        var results = res.data;
        var tmplabels = [],tmpdata = [];
        results.forEach(function(x) {
          tmplabels.push(x.id);
          tmpdata.push(parseFloat(x.sum));
        });

        var tempData = {
          labels: tmplabels,
          datasets: [
            {
              label: "Sum",
              data: tmpdata,
              borderColor: "rgb(75, 192, 192)",
              backgroundColor: "rgba(75, 192, 192, 0.2)"
            }
          ]
        };
        this.jsonchartdata = tempData;
        this.loaded = true;
      } catch (e) {
        console.error(e);
      }
  }
};
</script>
