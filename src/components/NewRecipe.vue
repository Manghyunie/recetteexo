<template>
    <div>
        Add a new recipe
        <br>
        <br>
      <div @keyup.enter="$emit('create-new-recipe', recipe)">
        <input type="text" placeholder="Enter a recipe name" v-model="recipe.newRecipeTitle" />
        <input type="text" placeholder="Enter a recipe description" v-model="recipe.newRecipeDesc" />
      </div>
      <br>
      <button @click="$emit('create-new-recipe', recipe)">Add</button>
    </div>
  </template>
  
  <script>
  export default {
    name: "NewRecipe",
    components: "",
    props: {},
    data() {
      return {
        recipe: {
          newRecipeTitle: "",
          newRecipeDesc: ""
        }
      };
    },
    methods: {
    },
    computed: {}
  };
  </script>
  
  <style></style>