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
          v-model="query"
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
          value="5"
          v-model="number"
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
          v-model="cuisine"
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
          v-model="diet"
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
          v-model="intolerance"
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
          v-model="watched"
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
          v-model="favorite"
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
    <!-- <b-form @submit.prevent="onSearch" @reset.prevent="onReset">
      <b-form-group
        id="input-group-username"
        label-cols-sm="3"
        label="Username:"
        label-for="username"
      >
        <b-form-input
          id="username"
          v-model="$v.form.username.$model"
          type="text"
          :state="validateState('username')"
        ></b-form-input>
        <b-form-invalid-feedback v-if="!$v.form.username.required">
          Username is required
        </b-form-invalid-feedback>
        <b-form-invalid-feedback v-else-if="!$v.form.username.length">
          Username length should be between 3-8 characters long
        </b-form-invalid-feedback>
        <b-form-invalid-feedback v-if="!$v.form.username.alpha">
          Username alpha
        </b-form-invalid-feedback>
      </b-form-group>

      <b-form-group
        id="input-group-country"
        label-cols-sm="3"
        label="Country:"
        label-for="country"
      >
        <b-form-select
          id="country"
          v-model="$v.form.country.$model"
          :options="countries"
          :state="validateState('country')"
        ></b-form-select>
        <b-form-invalid-feedback>
          Country is required
        </b-form-invalid-feedback>
      </b-form-group>

      <b-form-group
        id="input-group-Password"
        label-cols-sm="3"
        label="Password:"
        label-for="password"
      >
        <b-form-input
          id="password"
          type="password"
          v-model="$v.form.password.$model"
          :state="validateState('password')"
        ></b-form-input>
        <b-form-invalid-feedback v-if="!$v.form.password.required">
          Password is required
        </b-form-invalid-feedback>
        <b-form-text v-else-if="$v.form.password.$error" text-variant="info">
          Your password should be <strong>strong</strong>. <br />
          For that, your password should be also:
        </b-form-text>
        <b-form-invalid-feedback
          v-if="$v.form.password.required && !$v.form.password.length"
        >
          Have length between 5-10 characters long
        </b-form-invalid-feedback>
      </b-form-group>

      <b-form-group
        id="input-group-confirmedPassword"
        label-cols-sm="3"
        label="Confirm Password:"
        label-for="confirmedPassword"
      >
        <b-form-input
          id="confirmedPassword"
          type="password"
          v-model="$v.form.confirmedPassword.$model"
          :state="validateState('confirmedPassword')"
        ></b-form-input>
        <b-form-invalid-feedback v-if="!$v.form.confirmedPassword.required">
          Password confirmation is required
        </b-form-invalid-feedback>
        <b-form-invalid-feedback
          v-else-if="!$v.form.confirmedPassword.sameAsPassword"
        >
          The confirmed password is not equal to the original password
        </b-form-invalid-feedback>
      </b-form-group>

      <b-button type="reset" variant="danger">Reset</b-button>
      <b-button
        type="submit"
        variant="primary"
        style="width:250px;"
        class="ml-5 w-75"
        >Register</b-button
      >
      <div class="mt-2">
        You have an account already?
        <router-link to="login"> Log in here</router-link>
      </div>
    </b-form> -->


    <!-- <b-alert
      class="mt-2"
      v-if="form.submitError"
      variant="warning"
      dismissible
      show
    >
      Register failed: {{ form.submitError }}
    </b-alert> -->
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
  export default {
  name: "Search",
  data() {
    return {
      form: {
        query: "",
        cuisine: null,
        diet: null,
        intolerance: null,
        number: 5,
        watched: null,
        favorite: null,
        submitError: undefined
      },
      cuisines: [{ value: null, text: "", disabled: true }],
      diets: [{ value: null, text: "", disabled: true }],
      intolerances: [{ value: null, text: "", disabled: true }],
      amountRecipes: [{ value: null, text: "", disabled: true }],
      watchedAns: [{ value: null, text: "", disabled: true }],
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
    let numReturns = [5, 10, 15];
    let binaryAns = ["Yes", "No"];
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
          this.$root.store.server_domain + "/searchRecipes",

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