<template>
    <div>
      <!-- Using modifiers -->
      <b-button v-b-modal.my-modal>Create Recipe</b-button>

      <!-- The modal -->
      <b-modal id="my-modal">
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
        <b-form-group label="Vegeterian:" label-for="vegeterian">
          <input type="checkbox" id="vegeterian" v-model="vegeterian">
        </b-form-group>
        <b-form-group label="Gluten Free:" label-for="glutenFree">
          <input type="checkbox" id="glutenFree" v-model="glutenFree" >
        </b-form-group>
        <button @click="create">Create</button>
      </b-modal>
    </div>    
</template>

<script>
export default {
  name: "CreateRecipe",
  methods:{
    async create(event){
      if(!(!this.name || !this.picture || !this.time || !this.title || !this.ingridients || !this.instructions || !this.num) && (this.name.length>0 && this.picture.length>0 && this.time.length>0 && this.title.length>0 && this.ingridients.length>0 && this.instructions.length>0 && this.num.length>0)){
        let vegeterianInt=0;
        let glutenFreeInt=0;
        if(this.vegeterian){vegeterianInt=1;}
        if(this.glutenFree){glutenFreeInt=1;}
        const response = await this.axios.post(
          "http://localhost:3000/users/personal",
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
.container {
  max-width: 400px;
}
</style>
