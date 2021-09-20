<template>
  <v-app dark>
    <v-navigation-drawer v-model="drawer" clipped fixed app>
      <v-list>
        <v-list-item
          v-for="(item, i) in items"
          :key="i"
          :to="item.to"
          router
          exact
        >
          <v-list-item-action>
            <v-icon>{{ item.icon }}</v-icon>
          </v-list-item-action>
          <v-list-item-content>
            <v-list-item-title v-text="item.title" />
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>

    <v-app-bar clipped-left fixed app>
      <v-app-bar-nav-icon @click.stop="drawer = !drawer" />
      <img src="/logo_mfu.png" alt="user" />
      <v-toolbar-title v-text="title" />

      <v-spacer />

      <v-avatar>
        <img src="/account-circle.png" alt="user" />
      </v-avatar>
    </v-app-bar>

    <v-main>
      <v-container>
        <Nuxt />
      </v-container>
    </v-main>

    <v-footer :absolute="!fixed" app>
      <span>&copy; {{ new Date().getFullYear() }}</span>
    </v-footer>
  </v-app>
</template>

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
          title: "Welcome",
          to: "/",
        },
        {
          icon: "mdi-database",
          title: "Show data table",
          to: "/showdata",
        },
        {
          icon: "mdi-application-import",
          title: "Show Grahp",
          to: "/showgrahp",
        },
        {
          icon: "mdi-circle-outline",
          title: "null page",
          to: "/",
        },
      ],
      miniVariant: false,
      right: true,
      rightDrawer: false,
      title: "MAE FAH LUANG",
    };
  },
};
</script>
