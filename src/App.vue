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
      <v-container>
        <BlogEntry v-for="filename in ['001-ningbo', '002-ningbo']" :key="filename" :filename="filename"/>
      </v-container>
    </v-content>
  </v-app>
</template>

<script>
import MyMenu from './components/MyMenu'
import BlogEntry from "./components/BlogEntry";

export default {
  name: 'App',

  components: {
    MyMenu,
    BlogEntry
  },


  data: () => ({
  }),

  computed: {
    colorIfDark() {
      return (this.$store.state.darkEnabled) ? 'blue-grey lighten-3' : 'grey'
    }
  },
};


</script>
