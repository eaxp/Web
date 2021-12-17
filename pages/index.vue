<template>

  <div>
  
     
  <div >  
    <br /><br />
    <h1 align="center" >HELMET MONITORING FOR MFU CAMPUS</h1>
    <br /><br />
    <div>
      <v-row>
        <v-col cols="12" align="center">
          <h2 class="display-1">Number of motorcycle users wearing helmets</h2><br><br>
          <h3>Current Date & Time: {{currentDateTime()}}</h3><br><br><br>
          <v-row align="center">
            <v-col cols="2"></v-col>
            <v-col cols="3"><v-card color="green lighten-1"><br><img src="/racing-helmet.png" alt="user" /><br> <h3>Wear a helmet</h3>  <br> <h3 v-if="data">{{data[data.length-1].withhelmet}}</h3> <br></v-card></v-col>
            <v-col cols="2"></v-col>
            <v-col cols="3"><v-card color="red lighten-1"><br><img src="/face-man-profile.png" alt="user" /><br> <h3>Not wearing a helmet</h3><br> <h3 v-if="data">{{data[data.length-1].withouthelmet}}</h3> <br></v-card></v-col>
            <v-col cols="2"></v-col>
          </v-row>
        </v-col>    
      </v-row><br><br><br>
      <v-row>
        
            <v-col cols="2"></v-col>
            <v-col cols="8" align="center">
              <v-card >
                <bar-chart
                  :barchartdata="barchartdata"
                  :barchartoptions="barchartoptions"
                  :height="300"/>
              </v-card></v-col>
            <v-col cols="2"></v-col>
            
          
      </v-row>
      <br><br><br>
    </div>
    <br /><br /><br />
  </div>
  </div>
</template>
  
<script>

const url = "/aaaaa copy 2.json";
export default {
  data() {
    return {
      data: null,
      barchartdata: {
        labels: ["with helmet", "without helmet"],
        datasets: [
          { 
            label: " Data ",
            data: [60, 54],
            backgroundColor: [
              "rgba(102, 187, 106, 0.2)",
              "rgba(239, 83, 80, 0.2)",
            ],
            borderColor: [
              "rgba(102, 187, 106, 2)",
              "rgba(239, 83, 80, 2)",
            ],
            borderWidth: 2
          }
        ]
      },
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
    };
  },
  async mounted() {
    this.loaded = false;
    try {
      const res = await this.$axios.get(url);
      console.log(res.data);
      this.data = res.data;
      results.forEach(function(x) {
        tmplabels.push(x.date);
        tmpdata.push(parseFloat(x.sum));
      });
    } catch (e) {
      console.error(e);
    }
  },

  
  computed: {
    //computedDateFormatted() {
      //return this.formatDate(this.date);
    //},
    userLastCount() {
      return this.lineData[this.lineData.length - 1].data;
    },
  },

  watch: {
    date(val) {
      this.dateFormatted = this.formatDate(this.date);
    },
  },

  methods: {
    formatDate(date) {
      if (!date) return null;

      const [year, month, day] = date.split("-");
      return `${month}/${day}/${year}`;
    },
    parseDate(date) {
      if (!date) return null;

      const [month, day, year] = date.split("/");
      return `${year}-${month.padStart(2, "0")}-${day.padStart(2, "0")}`;
    },
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
    currentDate() {
      const current = new Date();
      const date =
        current.getDate() +
        "-" +
        (current.getMonth() + 1) +
        "-" +
        current.getFullYear();      
      const dateTime1 = date ;

      return dateTime1;
    },
  },
};
</script>

