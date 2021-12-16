<template>
  <div><br>
    <h1 >ตารางข้อมูลแสดงการสวมหมวกนิรภัยของผู้ใช้รถจักรยานยนต์</h1>
    <br>
    <!--<h2 v-if="data">--- {{data[0].date}} ---</h2><br>-->

    <v-card>
      <v-card-title>
        Data table
        <v-spacer></v-spacer>
        <v-text-field
          v-model="search"
          append-icon="mdi-magnify"
          label="Search"
          single-lin
          hide-details
        >
        </v-text-field>
      </v-card-title>
      <v-data-table
        :headers="headers1"
        :items="data"
        :search="search"
        v-if="data"
      >
      </v-data-table>
      
      <!--<v-card-title>
                Data table2
                    <v-spacer></v-spacer>
                        <v-text-field v-model="search" append-icon="mdi-magnify" label="Search"
                        single-lin hide-details >
                        </v-text-field>
            </v-card-title>
            <v-data-table :headers="headers1" :items="data1" :search="search1" v-if="data1">
            </v-data-table>-->
      <br></v-card><br><br>
  </div>
</template>
<script>
const url1 = "/datatest.json";
const url = "/aaaaa.json";

export default {
  data() {
    return {
      data: null,
      data1: null,
      search: "",
      search1: "",
      headers: [
        { text: "ID", align: "start", sortable: true, value: "id" },
        { text: "Sum", value: "sum" },
        { text: "Date", value: "date" },
      ],
      headers1: [
        { text: "Date", align: "start", sortable: true, value: "date" },
        { text: "With Helmet", value: "withhelmet" },
        { text: "Without Helmet", value: "withouthelmet" },
        { text: "Sum (With/Without Helmat)", value: "sum" },
      ],
    };
  },
  async mounted() {
    try {
      const res = await this.$axios.get(url);
      console.log(res.data);
      this.data = res.data;
    } catch (e) {
      console.error(e);
    }
  },
};
</script>