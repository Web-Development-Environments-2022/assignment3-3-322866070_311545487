<template>




  <div>
    <ol>
      <li v-for="(recipe,index) in this.recipes" :key="index">
        <h1>{{recipe.name}}</h1>
        <h2>{{recipe.title}}</h2>
        <b-card-img :src="recipe.picture"/>
        <br>
        <h3>Time To Prepare:</h3>
        <h3>{{recipe.time_to_prepare}}</h3>
        <h3>Gluten Free :{{recipe.glutenFree==1}}</h3>
        <h3>Vegeterian: {{recipe.vegeterian==1}}</h3>
        <br>
        <h3>Ingridients:</h3>
        <h4>{{recipe.ingridients}}</h4>
        <br>
        <h3>Instructions:</h3>
        <h4>{{recipe.instructions}}</h4>
        <br>
        <h3>Number Of Servings: {{recipe.number_of_servings}}</h3>
      </li>
    </ol>
    <button @click="updatePhotos">Create</button>
  </div>
</template>

<script>
export default {
  name: "About",
  data(){
    return{recipes:[]}
  },
  async created(){
    const response=await this.axios.get("http://localhost:3000/users/personal");
    this.recipes=response.data;
    updatePhotos();
    setTimeout(updatePhotos,5000);
  },
  updatePhotos(){
    alert(this.document);
    for(recipe in this.recipes){
      alert(document.getElementById('hello').outerHTML);

    }
  }
};
</script>
<style lang="scss" scoped>
.container {
  max-width: 400px;
}
</style>
