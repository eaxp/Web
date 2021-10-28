<template>
  <div>
    <v-row justify="center" align="center">
      <v-col cols="12">
        <br /><br /><br />
        <h3>Welcome to My project</h3>
        <br /><br /><br />
      </v-col>
    </v-row>
    <v-card align="center">
      <br /><br /><br />
      <b-container class="bv-example-row">
        <v-row>
          <v-col cols="2"></v-col>
          <v-col cols="8"><h1>HELMET MONITORING FOR MFU CAMPUS</h1></v-col>
          <v-col cols="2"></v-col>
        </v-row> </b-container
      ><br />

      <v-row>
        <v-col cols="7"></v-col
        >
        <v-col lg="3">
          <v-menu
            ref="menu1"
            v-model="menu1"
            :close-on-content-click="false"
            transition="scale-transition"
            offset-y
            max-width="290px"
            min-width="auto"
          >
            <template v-slot:activator="{ on, attrs }">
              <v-text-field
                v-model="dateFormatted"
                label="Date"
                hint="MM/DD/YYYY format"
                persistent-hint
                prepend-icon="mdi-calendar"
                v-bind="attrs"
                @blur="date = parseDate(dateFormatted)"
                v-on="on"
              ></v-text-field>
            </template>
            <v-date-picker
              v-model="date"
              no-title
              @input="menu1 = false"
            ></v-date-picker>
          </v-menu>
          <!--<p>Date in ISO format: <strong>{{ date }}</strong></p>-->
        </v-col>
        <v-col cols="2"><button>google</button></v-col>
      </v-row>
      

      <v-row>
        <v-col cols="6" align="center"><h2>Today's statistic of detect hearing a helmet</h2><br><br>
        <h3>Current Date & Time: {{currentDateTime()}}</h3><br><br><br>
        <v-row>
          <v-col cols="1"></v-col>
          <v-col cols="5"><v-card><br><br> aaa <br><br><br></v-card></v-col>
          <v-col cols="1"></v-col>
          <v-col cols="5"><v-card>bbb</v-card></v-col>
         
        </v-row></v-col>
        <v-col cols="5" align="center"> <br><br>
          <v-card>
          <bar-chart
            :barchartdata="barchartdata"
            :barchartoptions="barchartoptions"
            :height="300"
          />
        </v-card></v-col>
        <v-col cols="1"></v-col>
      </v-row>

      



      <br /><br /><br /><br /><br /><br />
      <h2>HELMET MONITORING FOR MFU CAMPUS</h2>
      <h3>Today's statistic of detect hearing a helmet</h3>

      <br /><br /><br /><br /><br /><br />
    </v-card>
    <br /><br /><br />
  </div>
</template>
  
<script>
const url = "/datahome.json";
export default {
  data() {
    return {
      value: "",
      barchartdata: {
        labels: ["Red", "Blue", "Yellow", "Green", "Purple", "Orange"],
        datasets: [
          {
            label: "# of Votes",
            data: [12, 19, 3, 5, 2, 3],
            backgroundColor: [
              "rgba(255, 99, 132, 0.2)",
              "rgba(54, 162, 235, 0.2)",
              "rgba(255, 206, 86, 0.2)",
              "rgba(75, 192, 192, 0.2)",
              "rgba(153, 102, 255, 0.2)",
              "rgba(255, 159, 64, 0.2)"
            ],
            borderColor: [
              "rgba(255, 99, 132, 1)",
              "rgba(54, 162, 235, 1)",
              "rgba(255, 206, 86, 1)",
              "rgba(75, 192, 192, 1)",
              "rgba(153, 102, 255, 1)",
              "rgba(255, 159, 64, 1)"
            ],
            borderWidth: 1
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
  data: (vm) => ({
    date: new Date(Date.now() - new Date().getTimezoneOffset() * 60000)
      .toISOString()
      .substr(0, 10),
    dateFormatted: vm.formatDate(
      new Date(Date.now() - new Date().getTimezoneOffset() * 60000)
        .toISOString()
        .substr(0, 10)
    ),
    menu1: false,
    menu2: false,
  }),

  computed: {
    computedDateFormatted() {
      return this.formatDate(this.date);
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
        current.getFullYear() +
        "-" +
        (current.getMonth() + 1) +
        "-" +
        current.getDate();
      const time =
        current.getHours() +
        " : " +
        current.getMinutes() +
        " : " +
        current.getSeconds();
      const dateTime = date + " " + time;

      return dateTime;
    },
  },
};

</script>

