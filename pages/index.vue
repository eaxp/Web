<template>
  <div>
    <br /><br />
    <h1 align="center">HELMET MONITORING FOR MFU CAMPUS</h1>
    <br /><br />
    <div>
      <v-row>
        <v-col cols="7" align="center">
          <h2>จำนวนการสวมหมวกนิรภัยของผู้ใช้รถจักรยานยนต์</h2><br><br>
          <h3>Current Date & Time: {{currentDateTime()}}</h3><br><br><br>
          <v-row>
            <v-col cols="1"></v-col>
            <v-col cols="5"><v-card><br><br> <h3>สวมหมวกนิรภัย</h3>  <br> <h3 v-if="data">{{data[49].withhelmat}}</h3> <br><br><br></v-card></v-col>
            <v-col cols="1"></v-col>
            <v-col cols="5"><v-card><br><br> <h3>ไม่สวมหมวกนิรภัย</h3><br> <h3 v-if="data">{{data[49].withouthelmat}}</h3> <br><br><br></v-card></v-col>
          </v-row>
        </v-col>
        <v-col cols="5" align="center"><br><br>
          <h3>show g ล่าสุด</h3><br><br>
          <v-row>
            <v-col align="center">
              <v-card v-if="loaded">
                <line-chart
                  :linechartdata="jsonchartdata"
                  :lineoptions="barchartoptions"
                  :height="130"
                />
              </v-card>
            </v-col>
          </v-row>
        </v-col>
      </v-row>
      <v-row>
        aaaaa
      </v-row>

    
      <br><br><br>
    </div>
    <br /><br /><br />
  </div>
</template>
  
<script>

const url = "/aaaaa copy.json";
export default {
  data() {
    return {
      data: null,
      value: "",
      jsonchartdata: {
        labels: [],
        datasets: [],
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
    try {
      const res = await this.$axios.get(url);
      console.log(res.data);
      this.data = res.data;
      return data
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
  },
};
</script>

