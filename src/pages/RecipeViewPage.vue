<template>
  <div class="container">
    <div v-if="this.recipe">
      <div class="recipe-header mt-3 mb-4">
        <h1 align="center">{{ recipe.title }}</h1>
        <img :src="recipe.image" class="center" align="center"/>
      </div>
      <div align="center">
        <strong><b-row>
          <b-col>Ready in {{ recipe.readyInMinutes }} Minutes</b-col>
          <b-col>Likes: {{ recipe.aggregateLikes }}</b-col>
          <b-col>Servings: {{ recipe.servings }}</b-col>
        </b-row></strong>
        <br>
      </div>
      <div class="recipe-body">
        <div class="wrapper" align="center">
          <div class="wrapped">
            <h4>Ingredients:</h4>
            <ul align="left">
              <li v-for="(r, index) in this.recipe.ingredients" :key="index">
                {{ r.original }}
              </li>
            </ul>
          </div>
          <div class="wrapped" >
            <h4>Instructions:</h4>
            <ol align="left">
              <li v-for="(r, index) in this.recipe._instructions" :key="index">
                {{ r.step }}

              </li>
              <!-- <li v-for="s in recipe._instructions" :key="s.number">
                {{ s.step }}
              </li> -->
            </ol>
          </div>
        </div>
      </div>
      <!-- <pre>
      {{ $route.params }}
      {{ recipe }}
    </pre
      > -->
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      recipe: null
    };
  },
  async created() {

    try {
      let response;
      // response = this.$route.params.response;

      try {
        response = await this.axios.get(
          // "https://test-for-3-2.herokuapp.com/recipes/info",
          // this.$root.store.server_domain + "/recipes/info",
          "http://localhost:3000/recipes/" + this.$route.params.recipeId ,
          // {
          //   params: { id: this.$route.params.recipeId }
          // }
        );

        console.log("response.status", response.status);
        if (response.status !== 200) this.$router.replace("/NotFound");
      } catch (error) {
        console.log("error.response.status", error.response.status);
        this.$router.replace("/NotFound");
        return;
      }

      let {
        analyzedInstructions,
        instructions,
        ingredients,
        aggregateLikes,
        readyInMinutes,
        servings,
        image,
        title
      } = response.data;

      // let _ingredients = parsedIngredients();
      // console.log("extendedIngredients " + ingredients);
      let _instructions = analyzedInstructions
        .map((fstep) => {
          fstep.steps[0].step = fstep.name + fstep.steps[0].step;
          return fstep.steps;
        })
        .reduce((a, b) => [...a, ...b], []);

      let _recipe = {
        instructions,
        _instructions,
        analyzedInstructions,
        ingredients,
        aggregateLikes,
        readyInMinutes,
        servings,
        image,
        title
      };

      this.recipe = _recipe;
    } catch (error) {
      console.log(error);
    }
  },
  // parsedIngredients() {
  //   ingredients = [];
  //   for (let i = 0; i < extendedIngredients.length; i++)
  //   {
  //       ingredients.push(extendedIngredients[i].amount + " " + extendedIngredients[i].unit + " of " + extendedIngredients[i].name);
  //   }
  //   return ingredients;
  // }
};
</script>

<style scoped>
.wrapper {
  display: flex;
}
.wrapped {
  width: 50%;
}
.center {
  display: block;
  margin-left: auto;
  margin-right: auto;
  width: 50%;
}
/* .recipe-header{

} */
</style>
