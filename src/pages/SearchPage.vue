<template>
  <div class="container" align="center">
    <h1 class="title" >Search Recipes</h1>
    <b-form @submit.prevent="onSearch" @reset.prevent="onReset">
      <b-form-group
          id="input-group-query"
          label-cols-sm="3"
          label="Search Query:"
          label-for="query"
        >
        <b-form-input
          id="query"
          type="text"
          v-model="$v.form.query"
        ></b-form-input>
      </b-form-group>

      <b-form-group
        id="input-group-number"
        label-cols-sm="3"
        label="Number:"
        label-for="number"
      >
        <b-form-select
          id="number"
          value=5 selected
          v-model="$v.form.number" 
          :options="amountRecipes"
        ></b-form-select>
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
          v-model="$v.form.cuisine"
          :options="cuisines"
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
          v-model="$v.form.diet"
          :options="diets"
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
          v-model="$v.form.intolerance"
          :options="intolerances"
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
          v-model="$v.form.watched"
          :options="watchedAns"
        ></b-form-select>
      </b-form-group>  

      <b-form-group
        id="input-group-favorite"
        label-cols-sm="3"
        label="Favorite:"
        label-for="favorite"
      >
        <b-form-select
          id="favorite"
          v-model="$v.form.favorite"
          :options="favoriteAns"
        ></b-form-select>
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
    <br>
  </div>
</template>

<script>
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
  const numReturns = [5, 10, 15];
  const binaryAns = ["Yes", "No"];
  export default {
  name: "Search",
  data() {
    return {
      form: {
        query: "",
        cuisine: null,
        diet: null,
        intolerance: null,
        number: "5",
        watched: null,
        favorite: null,
        submitError: undefined
      },
      cuisines: [{ value: null, text: "", disabled: true }],
      diets: [{ value: null, text: "", disabled: true }],
      intolerances: [{ value: null, text: "", disabled: true }],
      amountRecipes: [{ value: null, text: "", disabled: true }],
      watchedAns: [{ value: null, Number, disabled: true }],
      favoriteAns: [{ value: null, text: "", disabled: true }],
      errors: [],
      validated: false
    };
  },
  validations: {
    form: {
      number: {
        required
      }
      //   length: (u) => minLength(3)(u) && maxLength(8)(u),
      //   alpha
      // },
      // country: {
      //   required
      // },
      // password: {
      //   required,
      //   length: (p) => minLength(5)(p) && maxLength(10)(p)
      // },
      // confirmedPassword: {
      //   required,
      //   sameAsPassword: sameAs("password")
      // }
    }
  },
  mounted() {
    // console.log("mounted");

    this.cuisines.push(...cuisines);
    this.diets.push(...diets);
    this.intolerances.push(...intolerances);
    this.amountRecipes.push(...numReturns);
    this.watchedAns.push(...binaryAns);
    this.favoriteAns.push(...binaryAns);
    // console.log($v);
  },
  methods: {
    validateState(param) {
      const { $dirty, $error } = this.$v.form[param];
      return $dirty ? !$error : null;
    },
    async Search() {
      try {
        const response = await this.axios.post(
          // "https://test-for-3-2.herokuapp.com/user/Register",
          // this.$root.store.server_domain + "/searchRecipes",
          "http://localhost:3000/recipes/searchRecipes",

          {
            query: this.form.query,
            cuisine: this.form.cuisine,
            diet: this.form.diet,
            intolerance: this.form.intolerance,
            number: this.form.number,
            watched: this.form.watched,
            favorite: this.form.favorite
          }
        );
        this.$router.push("/recipesPreview");
        // console.log(response);
      } catch (err) {
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
        number: 5,
        watched: null,
        favorite: null
      };
      this.$nextTick(() => {
        this.$v.$reset();
      });
    },

  }
};
</script>

<style lang="scss" scoped>
.container {
  max-width: 500px;
}

</style>