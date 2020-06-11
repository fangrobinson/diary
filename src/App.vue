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
      <MyMenu v-on:trollear-jp="trollearJuampi"></MyMenu>
    </v-app-bar>

    <v-content>
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
    //
  }),


  methods: {
    trollearJuampi: function(){
      console.log("Event Captured");
      return { headerText: 'Te la creiste we ecsdi' };
    }
  },

};


</script>
