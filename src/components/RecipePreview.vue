<template>
  <span
    :to="{ name: 'recipe', params: { recipeId: recipe.id } }"
    class="recipe-preview"
  >

     <b-card v-if="this.image_load"
      :header="this.recipe.title"
      :img-src="this.recipe.image"
      img-alt="Image"
      img-top
      img-fluid="fluid"
      tag="article"
      style="max-width: 20rem;"
      class="mb-2"

    >
      <b-card-text id="data-content">
        <b-col>
          <!-- <b-row align="center">
          <h3 class="headline">{{recipe.title}}</h3>
          </b-row> -->

          <b-row align="left" style="padding-left: 10px;">
            <small>Ready In: {{ recipe.readyInMinutes }} Minutes </small>
            <!-- <b-col><small>Ready In: {{ recipe.readyInMinutes }} Minutes </small></b-col> -->
            <!-- <b-col><small>{{ recipe.aggregateLikes }} Likes </small></b-col> -->
            <!-- <b-col><small>{{ recipe.servings }} Servings </small></b-col> -->
          </b-row>
          <!-- <b-row align="left" style="padding-left: 10px;">
            <small>{{ recipe.aggregateLikes }} Likes </small>
          </b-row> -->
          <b-row align="left" style="padding-left: 10px;">
            <small>{{ recipe.servings }} Servings </small>
          </b-row>
          <b-row align="center" style="padding-left: 10px;">
            <!-- <small v-if="recipe.glutenFree"> Gluten Free </small> -->
            <!-- <b-col><small v-if="recipe.glutenFree"> Gluten Free </small></b-col>
            <b-col>
              <small v-if="recipe.vegan"> Vegan </small>
              <small v-else-if="recipe.vegetarian"> Vegetarian </small>
            </b-col> -->
            <b-col>
              <small>Gluten Free</small>
            </b-col>
            <b-col>
              <small v-if="recipe.vegan">Vegan</small>
              <small v-else>Vegetarian</small>
            </b-col>
            <!-- <b-col>
              <small>Vegetarian</small>
            </b-col> -->
          </b-row>
          <b-row align="center" style="padding-left: 10px;">
            <b-col>
              <small v-if="recipe.glutenFree"> V </small>
              <small v-else> X </small>
            </b-col>
            <b-col>
              <small v-if="recipe.vegan"> V </small>
              <small v-else-if="recipe.vegetarian"> V </small>
              <small v-else> X </small>
            </b-col>
            <!-- <b-col>
              <small v-if="recipe.vegetarian"> V </small>
              <small v-else> X </small>
            </b-col> -->
          </b-row>
          <!-- <b-row align="left" style="padding-left: 10px;">
            <small v-if="recipe.vegan"> Vegan </small>
            <small v-else-if="recipe.vegetarian"> Vegetarian </small>
          </b-row> -->
          <!-- <b-row align="left" style="padding-left: 10px;">
            <small v-if="recipe.vegetarian"> It's Vegetarian! </small>
          </b-row>                     -->
          </b-col>
      </b-card-text>
      <div align="center">
        <b-button variant="primary" :to="{ name: 'recipe', params: { recipeId: recipe.id } }" >See Recipe</b-button>
      </div>
      <br>
      <b-card-footer>{{ this.recipe.aggregateLikes }} Likes</b-card-footer>
    </b-card>
  </span>
</template>

<script>
export default {
  mounted() {
    this.axios.get(this.recipe.image).then((i) => {
      this.image_load = true;
    });
  },
  data() {
    return {
      image_load: false
    };
  },
  props: {
    recipe: {
      type: Object,
      required: true
    },

    id: {
      type: Number,
      required: true
    },
    title: {
      type: String,
      required: true
    },
    readyInMinutes: {
      type: Number,
      required: true
    },
    image: {
      type: String,
      required: true
    },
    aggregateLikes: {
      type: Number,
      required: false,
      default() {
        return undefined;
      }
    }
  }
};
</script>

<style scoped>
.recipe-preview {
  display: inline-block;
  width: 90%;
  height: 100%;
  position: relative;
  margin: 10px 10px;
}
.recipe-preview > .recipe-body {
  width: 100%;
  height: 200px;
  position: relative;
}

.recipe-preview .recipe-body .recipe-image {
  margin-left: auto;
  margin-right: auto;
  margin-top: auto;
  margin-bottom: auto;
  display: block;
  width: 98%;
  height: auto;
  -webkit-background-size: cover;
  -moz-background-size: cover;
  background-size: cover;
}

.recipe-preview .recipe-footer {
  width: 100%;
  height: 50%;
  overflow: hidden;
}

.recipe-preview .recipe-footer .recipe-title {
  padding: 10px 10px;
  width: 100%;
  font-size: 12pt;
  text-align: left;
  white-space: nowrap;
  overflow: hidden;
  -o-text-overflow: ellipsis;
  text-overflow: ellipsis;
}

.recipe-preview .recipe-footer ul.recipe-overview {
  padding: 5px 10px;
  width: 100%;
  display: -webkit-box;
  display: -moz-box;
  display: -webkit-flex;
  display: -ms-flexbox;
  display: flex;
  -webkit-box-flex: 1;
  -moz-box-flex: 1;
  -o-box-flex: 1;
  box-flex: 1;
  -webkit-flex: 1 auto;
  -ms-flex: 1 auto;
  flex: 1 auto;
  table-layout: fixed;
  margin-bottom: 0px;
}

.recipe-preview .recipe-footer ul.recipe-overview li {
  -webkit-box-flex: 1;
  -moz-box-flex: 1;
  -o-box-flex: 1;
  -ms-box-flex: 1;
  box-flex: 1;
  -webkit-flex-grow: 1;
  flex-grow: 1;
  width: 90px;
  display: table-cell;
  text-align: center;
}
</style>
