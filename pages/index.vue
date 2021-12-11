<template>
  <div>
    <br /><br />
    <h1 align="center">HELMET MONITORING FOR MFU CAMPUS</h1>
    <br /><br />
    <div>
      <v-row>
        <v-col cols="7" align="center">
          <h2>Today's statistic of detect hearing a helmet</h2><br><br>
          <h3>Current Date & Time: {{currentDateTime()}}</h3><br><br><br>
          <v-row>
            <v-col cols="1"></v-col>
            <v-col cols="5"><v-card><br><br> <h3>Wering Helmet</h3>  <br> XXX <br><br><br></v-card></v-col>
            <v-col cols="1"></v-col>
            <v-col cols="5"><v-card><br><br> <h3>Not Wering Helmet</h3>  <br> YYY  <br><br><br></v-card></v-col>
         
          </v-row>
        </v-col>
          
        
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
        <v-col cols="2"><button>Go</button></v-col>
      </v-row>
      

    
      </v-row><br><br><br>
    </div>
    <br /><br /><br />
  </div>
</template>
  
<script>
const url = "/datahome.json";
export default {
  data() {
    return {
      value: "",  
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

