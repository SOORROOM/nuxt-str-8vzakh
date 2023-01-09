<template>
  <v-app>
    <v-navigation-drawer
      v-model="drawer"
      temporary
      :location="$vuetify.display.mobile ? 'bottom' : 'left'"
    >
      <v-list nav dense rounded>
        <v-list-item
          v-for="item in items"
          :key="item.text"
          link
          :to="item.link"
          :prepend-icon="item.icon"
          :title="item.text"
        >
        </v-list-item
      ></v-list>
      <v-spacer></v-spacer>
      <div class="pa-2 d-flex justify-center">
        <v-switch
          inset
          density="compact"
          @click="themeModify"
          label="Dark mode"
          append-icon="mdi-weather-night"
          prepend-icon="mdi-white-balance-sunny"
        >
        </v-switch>
      </div>
    </v-navigation-drawer>
    <v-app-bar
      density="compact"
      :collapse="$vuetify.display.mobile"
    >
      <v-app-bar-nav-icon @click.stop="drawer = !drawer" />
      <v-icon class="mx-3" color="orange">mdi-compass</v-icon>
      <v-toolbar-title class="mr-5 align-center">
        <span class="title">Mon Site test</span>
      </v-toolbar-title>
      <v-spacer></v-spacer>
      <div>
        <v-btn text>Logout</v-btn>
      </div>
      <div>
        <v-btn key="login" text rounded to="/login" color="primary"
          >Login</v-btn
        >
        <v-btn key="register" text rounded to="/signup" color="primary"
          >Register</v-btn
        >
      </div>
    </v-app-bar>
    <v-main>
      <slot />
    </v-main>
    <v-footer color="primary" :absolute="$vuetify.display.mobile">
      <v-row justify="center" no-gutters>
        <v-btn
          v-for="item in items"
          :key="item.text + 'footer-link'"
          color="white"
          variant="text"
          rounded
          size="x-small"
          class="my-2"
          :to="item.link"
          >{{ item.text }}
        </v-btn>
        <v-col class="text-center white--text text-caption mt-4" cols="12">
          {{ new Date().getFullYear() }} — Nuxt & Vuetify - SOORROOM
        </v-col>
      </v-row>
    </v-footer>
  </v-app>
</template>

<style scoped></style>

<script>
import { useTheme } from 'vuetify';
export default {
  data: () => ({
    drawer: false,
    items: [
      { icon: 'mdi-home', text: 'Home', link: '/' },
      { icon: 'mdi-login', text: 'Login', link: '/login' },
      { icon: 'mdi-file-table-box', text: 'Table', link: '/data' },
      { icon: 'mdi-file-table-box', text: 'Signup', link: '/signup' },
      { icon: 'mdi-file-table-box', text: 'pdf', link: '/pdfThreejs' },
      { icon: 'mdi-file-table-box', text: 'test', link: '/test' },
      { icon: 'mdi-phone', text: 'Phone', link: '/phonecall' },
      {
        icon: 'mdi-card-account-details',
        text: 'contacts',
        link: '/contacts',
      },
      { icon: 'mdi-map', text: 'map', link: '/map' },
      { icon: 'mdi-drag', text: 'drag', link: '/drag' },
      { icon: 'mdi-drag', text: 'drag+', link: '/dragplus' },
      { icon: 'mdi-lock', text: 'admin', link: '/admin' },
    ],
  }),
  setup() {
    const theme = useTheme();

    return {
      theme,
      themeModify: () =>
        (theme.global.name.value = theme.global.current.value.dark
          ? 'light'
          : 'dark'),
    };
  },
  mounted() {
    console.log(this.$vuetify.display.mobile);
  },
  methods: {},
};
</script>
