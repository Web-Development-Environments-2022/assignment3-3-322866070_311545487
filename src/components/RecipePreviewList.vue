<template>
  <b-container>
    <h3>
      {{ title }}:
      <slot>
        <div v-if="this.randomRecipesList">
          <b-button @click="refresh()">Refresh</b-button>
        </div>
      </slot>
    </h3>
    <b-row>
      <b-col v-for="r in recipes" :key="r.id">
        <!-- {{ r.id }} -->
        <RecipePreview class="recipePreview" :recipe="r" />
      </b-col>
    </b-row>
    <br>
    
  </b-container>
</template>

<script>
import RecipePreview from "./RecipePreview.vue";
export default {
  name: "RecipePreviewList",
  components: {
    RecipePreview
  },
  props: {
    title: {
      type: String,
      required: true
    }
  },
  data() {
    return {
      recipes: [],
      randomRecipesList:false
    };
  },
  mounted() {
    if(this.title==="Random Recipes"){
      this.randomRecipesList=true
      this.updateRecipes();
    }
    else if (this.title==="Favorite Recipes"){
      this.favoriteRecipes();
    }

  },
  methods: {
    async updateRecipes() {
      try {
        const response = await this.axios.post(
          // this.$root.store.server_domain + "/recipes/randomRecipes",
          // "https://test-for-3-2.herokuapp.com/recipes/random"
           "http://localhost:3000/recipes/randomRecipes",
        );

        // console.log("this is the LOGGGG:  " + response.data);
        const recipesRes = response.data;
        this.recipes = [];
        this.recipes.push(...recipesRes);
        // console.log(this.recipes);
      } catch (error) {
        console.log(error);
      }
    },
    async favoriteRecipes() {
      try {
        const response = await this.axios.get(
          // this.$root.store.server_domain + "/recipes/randomRecipes",
          // "https://test-for-3-2.herokuapp.com/recipes/random"
           "http://localhost:3000/users/favorites"
        );

        console.log("this is the LOGGGG:  " + response.data);
        const recipesRes = response.data;
        this.recipes = [];
        this.recipes.push(...recipesRes);
        console.log("this.recipes " + this.recipes);
      } catch (error) {
        console.log(error);
      }
    },
    async refresh(){
      this.updateRecipes();
    }
  }
};
</script>

<style lang="scss" scoped>
.container {
  min-height: 400px;
}
</style>
