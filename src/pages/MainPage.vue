<template>
  <div class="container">
    <h1 class="title" align="center">Main Page</h1>
    <b-row>
      <b-col>
        <RecipePreviewList title="Random Recipes" class="RandomRecipes center" />
      </b-col>
      <b-col>
        <!-- <b-button v-if="!$root.store.username" to="/login" tag="button">You need to Login to vue this</b-button> -->
        <LoginPage v-if="!$root.store.username"/>

    <!--    <RecipePreviewList
          v-else
          title="Last Viewed Recipes"
          :class="{
            blur: !$root.store.username,
            center: true
          }"
          disabled
        ></RecipePreviewList>-->
      </b-col>
    </b-row>
    <!-- <div
      style="position: absolute;top: 70%;left: 50%;transform: translate(-50%, -50%);"
    >
      Centeredasdasdad
    </div>-->
  </div>
</template>

<script>
import RecipePreviewList from "../components/RecipePreviewList";
import LoginPage from "./LoginPage.vue";
export default {
  components: {
    RecipePreviewList,
    LoginPage
}
};
</script>

<style lang="scss" scoped>
.RandomRecipes {
  margin: 10px 0 10px;
}
.blur {
  -webkit-filter: blur(5px); /* Safari 6.0 - 9.0 */
  filter: blur(2px);
}
::v-deep .blur .recipe-preview {
  pointer-events: none;
  cursor: default;
}
</style>
