<template>
  <v-app>
    <v-app-bar
      app
      dense
      flat
      color="#3b3f42"
      :dark="$store.state.darkEnabled"
    >
      <div class="d-flex align-center">
        <v-avatar tile>
          <v-img
                  alt="Robinson Icon"
                  class="shrink mr-2"
                  contain
                  src="https://i.imgur.com/FJeOp8h.png"
                  transition="scale-transition"
                  width="40"
          />
        </v-avatar>
      </div>

      <v-spacer></v-spacer>
      <MyMenu/>
    </v-app-bar>
    <v-content :class="backgroundColor">
      <v-container>
        <BlogEntry v-for="filename in ['entry001', 'entry002', 'entry003', 'entry004']" :key="filename" :filename="filename"/>
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
    backgroundColor() {
      return (this.$store.state.darkEnabled) ? 'dark-background' : 'light-background'
    }
  },
};
</script>

<style>
  .dark-background {
    background-color: #2b2b2b;
  }
  .light-background {
    background-color: white;
  }
</style>