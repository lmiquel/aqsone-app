<template>
  <v-app>
    <v-app-bar
      app
      color="primary"
      dark
    >
      <div class="d-flex align-center">
        <h1>Recipe.net</h1>
      </div>

      <v-spacer></v-spacer>

    </v-app-bar>

    <v-main>
      <Intro/>
      <Recipes/>
    </v-main>
  </v-app>
</template>

<script>
import Intro from './components/Intro';
import Recipes from './components/Recipes';

export default {
  name: 'App',

  components: {
    Intro,
    Recipes,
  },

};
</script>
