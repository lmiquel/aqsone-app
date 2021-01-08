<template>
  <v-container>
      <v-text-field
        label="Type an ingredient"
        outlined
        v-model="ingredientName" />
      <div class="d-flex justify-space-between flex-wrap">
      <label for="vegan">Vegan
        <input type="checkbox" v-model="vegan" id="vegan" />
      </label>
      <label for="alcohol">Alcohol-free
        <input type="checkbox" v-model="alcohol" id="alcohol" />
      </label>
      <v-btn
        medium
        class="primary rounded-lg" 
        v-on:click="getRecipes()"
      >Go!</v-btn>
    </div>

      <ul class="d-flex justify-space-around flex-wrap text-decoration-none">
        <v-li class="rounded-lg text-decoration-none" v-for="post in posts" v-bind:key="post.recipe.label">
          <v-card class="rounded-lg">
          <h3 class="text-center">{{ post.recipe.label }}</h3>
          <img class="rounded-lg" v-bind:src="post.recipe.image" v-on:click="showModal = true"/>
          </v-card>
          <div v-if="showModal">
              <h3>{{ post.recipe.label }}</h3>
                <ul>
                  <li v-for="ingredient in post.recipe.ingredients" v-bind:key="ingredient.text">{{ ingredient.text }}</li>
                </ul>
                <v-btn 
                  medium
                  class="primary rounded-lg" 
                  v-on:click="showModal = false"
                >OK</v-btn>
            </div>
        </v-li>
      </ul>
  </v-container>
</template>

<script>

  export default {
    name: 'Recipes',

    data: () => ({
    ingredientName:"",
    showModal: false,
    posts: null,
    vegan: false,
    alcohol: false,
  }),

  methods:{
    getRecipes(){
      const axios = require('axios');
      let ingredientName = this.ingredientName;
      let alcohol = this.alcohol;
      let vegan = this.vegan;
      
      axios.get(`https://api.edamam.com/search?q=${ingredientName}&app_id=142d1575&app_key=e7e8f690eb0adae355b58919a5b04cef&from=0&to=20${alcohol === true ? "&health=alcohol-free" : ""}${vegan === true ? "&health=vegan" : ""}`)
      .then(res => this.posts = res.data.hits);
    }
  },
};
</script>
