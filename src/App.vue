<template>
  <v-app>
    <v-app-bar
      app
      color="green"
      dark
      height="90"
    >   

      <v-avatar
        size="80"
        color="green"
        class="mr-3"
      >
        <img :src="require('./assets/poppa.jpg')" alt="alt">
      </v-avatar>

      <h2>Poppa's Bus Stop App</h2>

    </v-app-bar>

    <v-main>
      <BusView></BusView>
    </v-main>

    <v-footer
      color="green"
      dark
      fixed
    >
      <v-avatar
        size="80"
        color="green"
        class="mr-3"
      >
        <img :src="require('./assets/charlotte.jpg')" alt="alt">
      </v-avatar>

      Design by Charlotte
    </v-footer>
  </v-app>
</template>

<script>
import BusView from './components/BusView'

export default {
  name: 'App',

  components: {
    BusView
  },

  data: () => ({
    //
  }),
};
</script>
