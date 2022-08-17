<template>
  <div class="container">
    <div v-if="this.recipe">
      <div class="recipe-header mt-3 mb-4">
        <h1 align="center">{{ recipe.title }}</h1>
        <img :src="recipe.image" class="center" align="center"/>
      </div>
      <div align="center">
        <b-row align="center" style="padding-left: 10px;">
            <b-col>
              <small>Gluten Free</small>
            </b-col>
            <b-col>
              <small v-if="recipe.vegan">Vegan</small>
              <small v-else>Vegetarian</small>
            </b-col>
          </b-row>
          <b-row align="center" style="padding-left: 10px;">
          <b-col>
            <small v-if="recipe.glutenFree"> &#10004; </small>
            <small v-else> &#10008; </small>
          </b-col>
          <b-col>
            <small v-if="recipe.vegan"> &#10004; </small>
            <small v-else-if="recipe.vegetarian"> &#10004; </small>
            <small v-else> &#10008; </small>
          </b-col>
        </b-row>
        <b-row align="center" style="padding-left: 10px;">
          <b-col><small>Watched</small></b-col>
          <b-col>
            <b-button v-if="isFavorite" variant="success" > Favorite</b-button>  <b-button v-else variant="danger" @click="favorite">Not Favorite</b-button>
          </b-col>
        </b-row>
        <b-row align="center" style="padding-left: 10px;">
          <b-col>
            <small v-if="!$root.store.username"> &#10008; </small>
            <!-- <small v-else-if="wasWatched"> &#10004; </small> -->
            <small v-else> &#10008; </small>
          </b-col>
          <b-col>
            <small v-if="!$root.store.username"> &#10008; </small>
            <small v-else-if="isFavorite"> &#10004; </small>
            <small v-else> &#10008; </small>
          </b-col>
        </b-row>
        <br>        
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
      recipe: null,
      isFavorite: false,
      recipes:[]
    };
  },
  methods:{
    async favorite(){
      const response=await this.axios.post("https://cookify.cs.bgu.ac.il/users/favorites",{
        recipeId:this.$route.params.recipeId
      });
      this.isFavorite=true;
    }
  },
  async created() {
    try {
      let response;
      // response = this.$route.params.response;
      try {
        response = await this.axios.get(
          //"http://localhost:443/recipes/" + this.$route.params.recipeId ,//remote:comment this
          "https://cookify.cs.bgu.ac.il/recipes/"+this.$route.params.recipeId,//local:comment this
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
      const response_recipes=await this.axios.get("https://cookify.cs.bgu.ac.il/users/favorites");
      this.recipes=response_recipes.data;
      for(let i=0;i<this.recipes.length;i++){
        if(this.recipes[i].id==this.$route.params.recipeId){
          this.isFavorite=true;
        }
      }
      let {
        analyzedInstructions,
        instructions,
        ingredients,
        aggregateLikes,
        readyInMinutes,
        servings,
        image,
        title,
        glutenFree,
        vegetarian,
        vegan
      } = response.data;
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
        title,
        glutenFree,
        vegetarian,
        vegan
      };

      this.recipe = _recipe;
    } catch (error) {
      console.log(error);
    }
  },
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
