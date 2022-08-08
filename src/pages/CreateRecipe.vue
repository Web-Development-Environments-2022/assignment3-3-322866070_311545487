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
        <b-form-group label="Time To Prepare:" label-for="time">
          <b-form-input id="time" v-model="time"></b-form-input>
        </b-form-group>        
        <b-form-group label="Ingridients:" label-for="ingredients">
          <b-form-input id="ingredients" v-model="Ingridients"></b-form-input>
        </b-form-group>        
        <b-form-group label="Instructions:" label-for="instructions">
          <b-form-input id="instructions" v-model="instructions"></b-form-input>
        </b-form-group>        
      </b-modal>
    </div>    
</template>

<script>
export default {
  name: "CreateRecipe"
};
</script>
<style lang="scss" scoped>
.container {
  max-width: 400px;
}
</style>
