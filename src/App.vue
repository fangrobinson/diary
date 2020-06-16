<template>
  <v-app>
    <v-app-bar
      app
      color="blue-grey lighten-3"
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
      <MyMenu @trollear-jp="trollearJuampi"></MyMenu>
    </v-app-bar>

    <v-content>
      <HelloWorld :header-text="headerText"/>
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
    headerText: 'Welcome to Vuetify',
  }),


  methods: {
    trollearJuampi() {
      console.log("Event Captured")
      this.headerText = 'Te la creiste we ecsdi'
    }
  },

};


</script>
