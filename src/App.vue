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
            <a class="nav-link" href="/main">Home <span class="sr-only">(current)</span></a>
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
          <li class="nav-item">
            <a class="nav-link" href="#/createrecipe">Create Recipe</a>
          </li>
          <li class="nav-item">
            <a class="nav-link" href="#/familyrecipes">Family Recipes</a>
          </li>
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
            <a class="nav-link" href="/main">Home <span class="sr-only">(current)</span></a>
          </li>
          <li class="nav-item">
            <a class="nav-link" href="#/search">Search</a>
          </li>
          <li>
            <b-nav-item-dropdown text="Personal">
              <b-dropdown-item href="#/favorites">Favorites</b-dropdown-item>
              <b-dropdown-item href="#/personal">My Recipes</b-dropdown-item>
              <b-dropdown-item href="#/familyrecipes">Family Recipes</b-dropdown-item>
            </b-nav-item-dropdown>
          </li>
          <li class="nav-item">
            <a class="nav-link" href="#/about">About</a>
          </li>
          <li class="nav-item">
            <a class="nav-link" href="#/createrecipe">Create Recipe</a>
          </li>
        </ul>
        <b-navbar-nav class="ml-auto">
          <b-nav-item-dropdown right>
            <!-- Using 'button-content' slot -->
            <template #button-content>
              <em>{{ $root.store.username }}</em>
            </template>
            <b-dropdown-item href="#/profile">My Profile</b-dropdown-item>
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
