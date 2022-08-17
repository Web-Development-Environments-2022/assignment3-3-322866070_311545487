<template>
  <div>
    <ul>
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
    </ul>
    <b-button v-b-modal.modal-create-recipe>Create Recipe</b-button>
    <b-modal align="center" id="modal-create-recipe" size="lg" title="Create Recipe" hide-footer>
      <b-form-group label="Recipe Name:" label-for="name">
        <b-form-input id="name" class="input-form" v-model="name"></b-form-input>
      </b-form-group>
      <b-form-group label="Recipe Title:" label-for="title">
        <b-form-input id="title" class="input-form" v-model="title"></b-form-input>
      </b-form-group>
      <b-form-group label="Recipe Picture (URL):" label-for="picture">
        <b-form-input id="picture" class="input-form" v-model="picture"></b-form-input>
      </b-form-group>
      <b-form-group label="Time To Prepare:" label-for="time">
        <b-form-input id="time" class="input-form" v-model="time"></b-form-input>
      </b-form-group>        
      <b-form-group label="Ingredients:" label-for="ingridients">
        <b-form-input id="ingridients" class="input-form" v-model="ingridients"></b-form-input>
      </b-form-group>        
      <b-form-group label="Instructions:" label-for="instructions">
        <b-form-input id="instructions" class="input-form" v-model="instructions"></b-form-input>
      </b-form-group>        
      <b-form-group label="Number Of Servings:" label-for="num">
        <b-form-input input id="num" class="input-form" v-model="num" ></b-form-input >
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
<!--    <button @click="updatePhotos">Create</button>-->
  </div>
</template>

<script>
export default {
  name: "MyRecipes",
  data(){
    return{recipes:[]}
  },
  methods:{
    async create(){
      if(!(!this.name || !this.picture || !this.time || !this.title || !this.ingridients || !this.instructions || !this.num) && (this.name.length>0 && this.picture.length>0 && this.time.length>0 && this.title.length>0 && this.ingridients.length>0 && this.instructions.length>0 && this.num.length>0)){
        let vegeterianInt=0;
        let glutenFreeInt=0;
        if(this.vegeterian){vegeterianInt=1;}
        if(this.glutenFree){glutenFreeInt=1;}
        const response = await this.axios.post(
  //          "http://localhost:3000/users/personal",//remote:comment this
          "https://cookify.cs.bgu.ac.il/users/personal",//local:comment this
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
        const updated=await this.axios.get("https://cookify.cs.bgu.ac.il/users/personal");
        this.recipes=updated.data;
        if(response.status==200){alert("Recipe Created Successfully")}
        else{alert("Recipe Already Exists");}
      }
      else{
        alert("Please Fill All the Fields");
      }
    }
  },
  async created(){
    const response=await this.axios.get("https://cookify.cs.bgu.ac.il/users/personal");
    this.recipes=response.data;
    updatePhotos();
    setTimeout(updatePhotos,5000);
  },
  updatePhotos(){
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
