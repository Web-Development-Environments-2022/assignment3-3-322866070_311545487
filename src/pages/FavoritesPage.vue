<template>
  <div class="container">
    <h1 class="title">Favorites:</h1>
    <b-row v-for="r in this.recipes" :key="r.id">
      <!-- {{ r.id }} -->
      <RecipePreview class="recipePreview" :recipe="r" />
    </b-row>
  </div>
</template>

<script>
import RecipePreview from "../components/RecipePreview";
export default {
    name: "FavoritesPage",
    data(){return{
      recipes:[]
    }},
     components: {
         RecipePreview
     },
    async created(){
      const response_recipes=await this.axios.get("https://cookify.cs.bgu.ac.il/users/favorites");
      this.recipes=response_recipes.data;
    }
};
</script>

<style lang="scss" scoped>
</style>