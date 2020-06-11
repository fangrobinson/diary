<template>
  <v-app>
    <v-app-bar
      app
      color="blue-grey lighten-3"
      dense="true"
      dark
    >
      <div class="d-flex align-center">
        <v-img
          alt="Robinson Icon"
          class="shrink mr-2"
          contain
          src="https://i.imgur.com/FJeOp8h.png"
          transition="scale-transition"
          width="40"
        />
      </div>

      <v-spacer></v-spacer>

      <v-spacer></v-spacer>

      <v-app-bar-nav-icon @click="drawer = !drawer"></v-app-bar-nav-icon>
    </v-app-bar>

    <v-navigation-drawer app v-model="drawer" class="blue-grey lighten-3" right="true" temporary>
      <p>test</p>
    </v-navigation-drawer>

    <v-content>
      <v-row align="center"><MyMenu></MyMenu></v-row>
      <HelloWorld/>
    </v-content>
  </v-app>
</template>

<script>
import HelloWorld from './components/HelloWorld';
import MyMenu from "./components/MyMenu";

export default {
  name: 'App',

  components: {
    HelloWorld,
    MyMenu,
  },

  data: () => ({
    drawer: false,
  }),
};
</script>
