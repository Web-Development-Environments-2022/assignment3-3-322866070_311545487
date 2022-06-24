<template>
  <div>
    <div  align="center">
      <h1 class="title" >Search Recipes</h1>
      <b-form class="container" @submit.prevent="onSearch" @reset.prevent="onReset" style="max-width: 500px;" >
        <b-form-group
            id="input-group-query"
            label-cols-sm="3"
            label="Search Query:"
            label-for="query"
            
          >
          <b-form-input
            id="query"
            type="text"
            v-model="$v.form.query.$model"
            :state="validateState('query')"
          ></b-form-input>
        </b-form-group>

        <b-form-group
          id="input-group-amount"
          label-cols-sm="3"
          label="Number:"
          label-for="amount"
        >
          <b-form-select
            id="amount"
            v-model.number="$v.form.amount.$model"
            :state="validateState('amount')"
          >
            <option value="5">5</option>
            <option value="10">10</option>
            <option value="15">15</option>
          </b-form-select>
          <b-form-invalid-feedback>
            Number of recipes is required
          </b-form-invalid-feedback>

        </b-form-group>
        <b-form-group
          id="input-group-cuisine"
          label-cols-sm="3"
          label="Cuisine:"
          label-for="cuisine"
        >
          <b-form-select
            id="cuisine"
            v-model="$v.form.cuisine.$model"
            :options="cuisines"
            :state="validateState('cuisine')"
          ></b-form-select>
        </b-form-group>

        <b-form-group
          id="input-group-diet"
          label-cols-sm="3"
          label="Diet:"
          label-for="diet"
        >
          <b-form-select
            id="diet"
            v-model="$v.form.diet.$model"
            :options="diets"
            :state="validateState('diet')"
          ></b-form-select>
        </b-form-group>

        <b-form-group
          id="input-group-intolerances"
          label-cols-sm="3"
          label="Intolerances:"
          label-for="intolerances"
        >
          <b-form-select
            id="intolerances"
            v-model="$v.form.intolerance.$model"
            :options="intolerances"
            :state="validateState('intolerance')"
          ></b-form-select>
        </b-form-group>

        <b-form-group
          id="input-group-watched"
          label-cols-sm="3"
          label="Watched:"
          label-for="watched"
        >
          <b-form-select
            id="watched"
            v-model="$v.form.watched.$model"
            :state="validateState('watched')"
          >
            <option value="1">Yes</option>
            <option value="0">No</option>
          </b-form-select>
        </b-form-group>  

        <b-form-group
          id="input-group-favorite"
          label-cols-sm="3"
          label="Favorite:"
          label-for="favorite"
        >
          <b-form-select
            id="favorite"
            v-model="$v.form.favorite.$model"
            :state="validateState('favorite')"
          >
            <option value="1">Yes</option>
            <option value="0">No</option>
          </b-form-select>
        </b-form-group>     
        
        <b-button type="reset" variant="danger" style="margin-right: 4px;">Reset</b-button>
        <!-- <b-button v-if="advSearch === true" type="advance_search" variant="secondary" v-on:click="advSearch = false">Advance Search</b-button> -->
        <b-button
          type="submit"
          variant="primary"
          style="width:250px;
                margin-left: 4px;"
          >Search</b-button
        >   
      </b-form>
          
      <br>

    </div>
    <div v-if="recipes"  align="center">
      <div v-if="recipes.length > 0" class="search-results" align="center" >
        <b-container>
          <h3>
            Search Results:          
          </h3>
            <b-form-group
              id="input-group-sort"
              label-cols-sm="3"
              label="Sort By:"
              label-for="sortBy"
              style="max-width: 300px;"
            >
              <b-form-select
                id="sortBy"
                v-model="$v.form.sortBy.$model"
                :state="validateState('sortBy')"
                v-on:change="sortHandler"
              >
                <option value="time">Preparation time</option>
                <option value="like">Likes</option>
              </b-form-select>
            </b-form-group>
          <b-col>
            <b-row v-for="r in recipes" :key="r.id">
              <!-- {{ r.id }} -->
              <SearchResultPreview class="recipePreview" :recipe="r" />
            </b-row>
          </b-col>
        </b-container>
        <br>
      </div>
      <div v-else align="center">
          <h3>
            No Results
            <slot></slot>
          </h3>
      </div>
    </div>
  </div>
</template>

<script>
  import SearchResultPreview from "../components/SearchResultPreview";
  import cuisines from "../assets/cuisines";
  import diets from "../assets/diets";
  import intolerances from "../assets/intolerances";
  import {
    required,
    minLength,
    maxLength,
    alpha,
    sameAs,
    email
  } from "vuelidate/lib/validators";
  // const numReturns = ["5", "10", "15"];
  // const binaryAns = ["Yes", "No"];

  export default {
  name: "Search",
  data() {
    return {
      form: {
        query: "",
        cuisine: null,
        diet: null,
        intolerance: null,
        amount: "5",
        watched: null,
        favorite: null,
        sortBy: null,
        submitError: undefined
      },
      cuisines: [{ value: null, text: "", disabled: true }],
      diets: [{ value: null, text: "", disabled: true }],
      intolerances: [{ value: null, text: "", disabled: true }],
      // amountRecipes: [{ value: null, text: "", disabled: true }],
      // watchedAns: [{ value: null, text: "", disabled: true }],
      // favoriteAns: [{ value: null, text: "", disabled: true }],
      errors: [],
      recipes: null,
      validated: false
    };
  },
  validations: {
    form: {
      query: {
        alpha
      },
      cuisine: {

      },
      diet: {

      },
      intolerance: {

      },
      amount: {
        required
      },
      watched: {

      },
      favorite: {

      },
      sortBy: {

      }
    }
  },
  components: {
    SearchResultPreview
  },
  mounted() {
    // console.log("mounted");

    this.cuisines.push(...cuisines);
    this.diets.push(...diets);
    this.intolerances.push(...intolerances);
    // this.amountRecipes.push(...numReturns);
    // this.watchedAns.push(...binaryAns);
    // this.favoriteAns.push(...binaryAns);
    // console.log($v);
  },
  methods: {
    validateState(param) {
      const { $dirty, $error } = this.$v.form[param];
      return $dirty ? !$error : null;
    },
    async Search() {
      try {
        // let resExist = false;
        const response = await this.axios.post(
          // "https://test-for-3-2.herokuapp.com/user/Register",
          // this.$root.store.server_domain + "/searchRecipes",
          "http://localhost:3000/recipes/searchRecipes",

          {
            query: this.form.query,
            cuisine: this.form.cuisine,
            diet: this.form.diet,
            intolerance: this.form.intolerance,
            amount: parseInt(this.form.amount),
            watched: parseInt(this.form.watched),
            favorite: parseInt(this.form.favorite)
          }
        );
        console.log("query: " + this.form.query);
        console.log("cuisine: " + this.form.cuisine);
        console.log("amount: " + this.form.amount);
        console.log("watched: " + this.form.watched);
        console.log("favorite: " + this.form.favorite);
        // this.$router.push("/RecipePreviewList");
        console.log(response);
        // isFound = true;
        const recipesRes = response.data;
        // if(this.recipes){
        //   resExist = true;
        // }
        this.recipes = [];
        this.recipes.push(...recipesRes);
        // console.log("this.form.sortBy: " + this.form.sortBy);
        if(this.form.sortBy){
          this.sortHandler(this.form.sortBy);
        }
        console.log("this.recipes " + this.recipes);
      } catch (err) {
        // isFound = false;
        console.log(err.response);
        this.form.submitError = err.response.data.message;
      }
    },
    onSearch() {
      // console.log("register method called");
      this.$v.form.$touch();
      if (this.$v.form.$anyError) {
        return;
      }
      // console.log("register method go");
      this.Search();
    },
    onReset() {
      this.form = {
        query: "",
        cuisine: null,
        diet: null,
        intolerance: null,
        amount: "5",
        watched: null,
        favorite: null,
        sortBy: null
      };
      this.$nextTick(() => {
        this.$v.$reset();
      });
    },
    sortHandler(event) {
      if (event === "time") {
        this.recipes.sort((a, b) => {
          return a.readyInMinutes < b.readyInMinutes ? -1 : 1;
        });
      }
      if (event === "like") {
        this.recipes.sort((a, b) => {
          return a.aggregateLikes > b.aggregateLikes ? -1 : 1;
        });
      }
    }
  }
};
</script>

<style lang="scss" scoped>
// .container {
  // max-width: max-content;
  // max-width: 500px;
// }

// .search-results{
  // max-width: 10000px;
// }
</style>