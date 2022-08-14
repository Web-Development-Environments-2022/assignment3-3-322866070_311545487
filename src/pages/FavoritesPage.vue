<template>
  <div class="container">
    <h1 class="title">Favorites:</h1>
    <RecipePreviewList title="Favorite Recipes" class="FavoritesPage center" />
  </div>
</template>

<script>
import RecipePreviewList from "../components/RecipePreviewList";
export default {
    name: "FavoritesPage",
    components: {
        RecipePreviewList
    }
};
</script>

<style lang="scss" scoped>

</style>