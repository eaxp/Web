<template>

<div>
  
  <v-app
    dark
    v-bind:style="{ background: $vuetify.theme.themes.dark.background }"
   
  >

    <v-navigation-drawer
      v-model="drawer"
      clipped
      fixed
      app
      color="amber lighten-3"
    >
      <v-list>
        <v-list-item
          v-for="(item, i) in items"
          :key="i"
          :to="item.to"
          router
          exact
        >
          <v-list-item-action style="color: #881518">
            <v-icon>{{ item.icon }}</v-icon>
          </v-list-item-action>
          <v-list-item-content>
            <v-list-item-title v-text="item.title" style="Libre Baskerville"/>
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>

    <v-app-bar clipped-left fixed app color="red darken-3">
      <v-app-bar-nav-icon @click.stop="drawer = !drawer" />
      <img src="/logo_mfu.png" alt="user" />
      <v-toolbar-title v-text="title" />

      <v-spacer />
    </v-app-bar>

    <v-main>
      <v-container>
        <Nuxt />
      </v-container>
    </v-main>
  </v-app>
  </div>
</template>


<script src="https://apis.google.com/js/platform.js" async defer></script>
<script>

export default {
  data() {
    return {
      clipped: false,
      drawer: false,
      fixed: false,
      items: [
        {
          icon: "mdi-account-details",
          title: "หน้าหลัก",
          to: "/",
        },
        {
          icon: "mdi-database",
          title: "ตารางข้อมูล",
          to: "/showdata",
        },
        {
          icon: "mdi-chart-pie ",
          title: "แดชบอร์ด",
          to: "/showgrahp",
        },
      ],

      miniVariant: false,
      right: true,
      rightDrawer: false,
      title: "HELMET MONITORING",
    };
  },
};
</script>
