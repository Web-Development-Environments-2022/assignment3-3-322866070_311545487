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
    <b-col>
      <b-row v-for="r in recipes" :key="r.id">
        <!-- {{ r.id }} -->
        <RecipePreview class="recipePreview" :recipe="r" />
      </b-row>
    </b-col>
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
    else if (this.title==="Last Viewed Recipes"){
      this.lastWatched();
    }
  },
  methods: {
    async updateRecipes() {
      try {
        const response = await this.axios.post(
           //"http://localhost:3000/recipes/randomRecipes",//remote:comment this
           "https://cookify.cs.bgu.ac.il/recipes/randomRecipes",//local:comment this
        );
        const recipesRes = response.data;
        this.recipes = [];
        this.recipes.push(...recipesRes);
      } catch (error) {
        console.log(error);
      }
    },
    async favoriteRecipes() {
      try {
        const response = await this.axios.get(
           //"http://localhost:3000/users/favorites"//remote:comment this
           "https://cookify.cs.bgu.ac.il/favorites",//local:comment this
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
