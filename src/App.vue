<template>
  <div id="app">
          <!-- <a class="navbar-brand" href="#">
        <img src="./assets/logo_main_2.png" width="150" height="50" class="d-inline-block align-top" alt="" loading="lazy">
        Cookify
      </a> -->
   <nav class="navbar navbar-expand-lg navbar-light bg-light" v-if="!$root.store.username">
      <a class="navbar-brand" href="/main">
        <img src="./assets/logo_main_2.png" width="150" height="50" class="d-inline-block align-top" alt="" loading="lazy">
      </a>
      <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
        <span class="navbar-toggler-icon"></span>
      </button>

      <div class="collapse navbar-collapse" id="navbarSupportedContent">
        <ul class="navbar-nav mr-auto">
          <li class="nav-item active">
<!--            <a class="nav-link" href="/main">Home <span class="sr-only">(current)</span></a> -->   <!--remote:comment this-->
            <a class="nav-link" href="/#/">Home <span class="sr-only">(current)</span></a>   <!--local:comment this-->
          </li>
          <li class="nav-item">
            <a class="nav-link" href="#/search">Search</a>
          </li>
          <li class="nav-item">
            <a class="nav-link" href="#/register">Register</a>
          </li>
          <li class="nav-item">
            <a class="nav-link" href="#/login">Login</a>
          </li>
          <li class="nav-item">
            <a class="nav-link" href="#/about">About</a>
          </li>
          <!-- <li class="nav-item">
            <a class="nav-link" href="#/createrecipe">Create Recipe</a>
          </li>
          <li class="nav-item">
            <a class="nav-link" href="#/familyrecipes">Family Recipes</a>
          </li> -->
        </ul>
        Welcome Guest
      </div>
    </nav>

   <nav class="navbar navbar-expand-lg navbar-light bg-light" v-else> <!-- v-else -->
      <a class="navbar-brand" href="#">
        <img src="./assets/logo_main_2.png" width="150" height="50" class="d-inline-block align-top" alt="" loading="lazy">
      </a>
      <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
        <span class="navbar-toggler-icon"></span>
      </button>

      <div class="collapse navbar-collapse" id="navbarSupportedContent">
        <ul class="navbar-nav mr-auto">
          <li class="nav-item active">
<!--            <a class="nav-link" href="/main">Home <span class="sr-only">(current)</span></a> --> <!--remote:comment this-->
            <a class="nav-link" href="/#">Home <span class="sr-only">(current)</span></a> <!--local:comment this-->
          </li>
          <li class="nav-item">
            <a class="nav-link" href="#/search">Search</a>
          </li>
          <li>
            <b-nav-item-dropdown text="Personal">
              <b-dropdown-item href="#/favorites">Favorites</b-dropdown-item>
              <b-dropdown-item href="#/myrecipes">My Recipes</b-dropdown-item>
              <b-dropdown-item href="#/familyrecipes">Family Recipes</b-dropdown-item>
            </b-nav-item-dropdown>
          </li>

          <!-- <li class="nav-item">
            <a class="nav-link" v-b-modal.modal-create-recipe>Create Recipe</a>
            <b-modal id="modal-create-recipe" size="lg" title="Create Recipe" hide-footer>
              <b-form-group label="Recipe Name:" label-for="name">
                <b-form-input id="name" v-model="name"></b-form-input>
              </b-form-group>
              <b-form-group label="Recipe Title:" label-for="title">
                <b-form-input id="title" v-model="title"></b-form-input>
              </b-form-group>
              <b-form-group label="Recipe Picture(URL):" label-for="picture">
                <b-form-input id="picture" v-model="picture"></b-form-input>
              </b-form-group>
              <b-form-group label="Time To Prepare:" label-for="time">
                <b-form-input id="time" v-model="time"></b-form-input>
              </b-form-group>        
              <b-form-group label="Ingridients:" label-for="ingridients">
                <b-form-input id="ingridients" v-model="ingridients"></b-form-input>
              </b-form-group>        
              <b-form-group label="Instructions:" label-for="instructions">
                <b-form-input id="instructions" v-model="instructions"></b-form-input>
              </b-form-group>        
              <b-form-group label="Number Of Servings:" label-for="num">
                <b-form-input input id="num" v-model="num" ></b-form-input >
              </b-form-group>
              <b-row>
                <b-col align="center">
                  <b-form-group label="Vegeterian:" label-for="vegeterian">
                    <input type="checkbox" id="vegeterian" v-model="vegeterian"/>
                  </b-form-group>
                </b-col>
                <b-col align="center">
                  <b-form-group label="Gluten Free:" label-for="glutenFree">
                    <input type="checkbox" id="glutenFree" v-model="glutenFree"/>
                  </b-form-group>
                </b-col>
              </b-row>
              <b-row><b-col align="center"><b-button @click="create">Create</b-button></b-col></b-row>
              
            </b-modal>
          </li> -->
          <li class="nav-item">
            <!-- <a class="nav-link" href="#/about">About</a> -->
            <a class="nav-link" v-b-modal.modal-1 >About</a>
            <b-modal id="modal-1" size="lg" title="Welcome to Cookify!" ok-only>
              <p class="my-4" align="center">The website was made by Yonatan Abeksis (311545487) and Shahar Cohen (322866070)</p>
              <p class="my-4" align="center">
                <b-link href="https://github.com/Web-Development-Environments-2022/assignment2-311545487_322866070" class="card-link">PacMan (Assignment 2)</b-link>
                <b-link href="https://github.com/Web-Development-Environments-2022/assignment3_2-322866070_311545487" class="card-link">Backend (Assignment 3_2)</b-link>
              </p>
            </b-modal>
          </li>
        </ul>
        <b-navbar-nav class="ml-auto">
          <b-nav-item-dropdown right>
            <!-- Using 'button-content' slot -->
            <template #button-content>
              <em>{{ $root.store.username }}</em>
            </template>
            <b-dropdown-item href="#/profile">My Profile</b-dropdown-item>
            <b-dropdown-item href="#/myrecipes">My Recipes</b-dropdown-item>
            <b-dropdown-item href="#/familyrecipes">Family Recipes</b-dropdown-item>
            <b-dropdown-item @click="Logout">Logout</b-dropdown-item>
            <!-- <b-dropdown-item>{{ $root.store.username }}: <button @click="Logout">Logout</button></b-dropdown-item> -->
          </b-nav-item-dropdown>
        </b-navbar-nav>
      </div>
    </nav>
    
    <!-- <div id="nav">
      <router-link :to="{ name: 'main' }">Vue Recipes</router-link>|
      <router-link :to="{ name: 'search' }">Search</router-link>|
      <router-link :to="{ name: 'about' }">About</router-link>|
      <router-link :to="{ name: 'createrecipe' }">Create Recipe</router-link>|
      {{ !$root.store.username }}
      <span v-if="!$root.store.username">
        Guest:
        <router-link :to="{ name: 'register' }">Register</router-link>|
        <router-link :to="{ name: 'login' }">Login</router-link>|
      </span>
      <span v-else>
        {{ $root.store.username }}: <button @click="Logout">Logout</button>|
      </span>
    </div> -->

    <router-view />
  </div>
</template>

<script>

export default {
  name: "App",
  methods: {
    Logout() {
      this.$root.store.logout();
      this.$root.toast("Logout", "User logged out successfully", "success");

      this.$router.push("/").catch(() => {
        this.$forceUpdate();
      });
    },
    async create(event){
      if(!(!this.name || !this.picture || !this.time || !this.title || !this.ingridients || !this.instructions || !this.num) && (this.name.length>0 && this.picture.length>0 && this.time.length>0 && this.title.length>0 && this.ingridients.length>0 && this.instructions.length>0 && this.num.length>0)){
        let vegeterianInt=0;
        let glutenFreeInt=0;
        if(this.vegeterian){vegeterianInt=1;}
        if(this.glutenFree){glutenFreeInt=1;}
        const response = await this.axios.post(
//          "http://localhost:3000/users/personal", //remote:comment this
          "https://cookify.cs.bgu.ac.il/users/personal", //local:comment this
          {
            picture:this.picture,
            name:this.name,
            time_to_prepare:this.time,
            title:this.title,
            vegeterian:vegeterianInt,
            ingridients:this.ingridients,
            instructions:this.instructions,
            number_of_servings:this.num,
            glutenFree:glutenFreeInt
          }
        );
        if(response.status==200){alert("Recipe Created Successfully")}
        else{alert("Recipe Already Exists");}
      }
      else{
        alert("Please Fill All the Fields");
      }
    }
  }
};
</script>

<style lang="scss" scoped>
@import "@/scss/form-style.scss";

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  min-height: 100vh;
}

#nav {
  padding: 30px;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
}

#nav a.router-link-exact-active {
  color: #42b983;
}
</style>
