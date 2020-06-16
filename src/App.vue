<template>
  <v-app>
    <v-app-bar
      app
      dense
      flat
      :color="colorIfDark"
      :dark="$store.state.darkEnabled"
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
      <MyMenu/>
    </v-app-bar>

    <v-content>
      <HelloWorld/>
    </v-content>
  </v-app>
</template>

<script>
import HelloWorld from './components/HelloWorld'
import MyMenu from './components/MyMenu'
import entry1 from './assets/entries/001-ningbo.json'

export default {
  name: 'App',

  components: {
    HelloWorld,
    MyMenu,
  },


  data: () => ({
  }),

  computed: {
    colorIfDark() {
      console.log(entry1.body)
      return (this.$store.state.darkEnabled) ? 'blue-grey lighten-3' : 'grey'
    }
  },
};


</script>
