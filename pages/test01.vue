<template>
  <div>
    <br /><br />
      <h1 align="center">HELMET MONITORING FOR MFU CAMPUS</h1>
    <br /><br />
    <!--<h1 v-if="data">{{data[data.length - 1].sum}}</h1>-->
    <v-row>
      <v-col cols="12" align="center"><h2>Number of motorcycle users wearing helmets</h2></v-col>
      <v-row>
        <v-col cols="12" align="center"><br><br><h3>Current Date & Time: {{ currentDateTime() }}</h3></v-col>
      </v-row>
    </v-row>
    <br><br><br>
    <v-row>
      <v-col v-cols="2" align="center">aa</v-col>
      <v-col v-cols="3" align="center">
        <v-card color="green lighten-1"><br/>
          <img src="/racing-helmet.png" alt="user"/><br/>
            <h3>Wear a helmet</h3><br/>
              <h3 v-if="data">{{ data[data.length - 1].withhelmet }}</h3><br />
        </v-card>
        </v-col>
      <v-col v-cols="2" align="center">aa</v-col>
      <v-col v-cols="3" align="center">
        <v-card color="red lighten-1"><br />
          <img src="/face-man-profile.png" alt="user" /><br />
            <h3>Not wearing a heslmet</h3><br />
              <h3 v-if="data">{{ data[data.length - 1].withouthelmet }}</h3><br />
              </v-card>
        </v-col>
      <v-col v-cols="2" align="center">aa</v-col>
    </v-row>
    <br><br><br>  
    <v-row>
      <v-col md="6">
        <v-card v-if="loaded">        
          <bar-chart
            :barchartdata="jsonchartdata"
            :barchartoptions="barchartoptions"
            :height="400"/>
        </v-card>
      </v-col>
      <v-col md="6">
        <v-card v-if="loaded">        
          <bar-chart
            :barchartdata="jsonchartdata2"
            :barchartoptions="barchartoptions"
            :height="400"/>
        </v-card>
      </v-col>
    </v-row>
    ------------------------------
  </div>
</template>

<script>
const url = "/aaa20.json";
const url1 = "/aaa20 copy.json";
const url3 = "detection.json";

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
      jsonchartdata2: {
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
      const res1 = await this.$axios.get(url3);
      
      var results1 = res1.data;
      var tmplabels2 = [],tmpdata2 = [];
      results1.forEach(function(x) {
        tmplabels2.push(x.date);
        tmpdata2.push(parseFloat(x.sum));
      });

      var tempData = {
        labels: tmplabels,
        datasets: [
          {
            label: "withhelmet by date",
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
            label: "sum by date",
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
  methods: {
        currentDateTime() {
      const current = new Date();
      const date =
        current.getDate() +
        "-" +
        (current.getMonth() + 1) +
        "-" +
        current.getFullYear();
      const time =
        current.getHours() +
        " : " +
        current.getMinutes() +
        " : " +
        current.getSeconds();
      const dateTime = date + "  " + time;

      return dateTime;
    },
  },
};
</script>
