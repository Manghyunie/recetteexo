<template>
  <div class="hello">
    <new-recipe @create-new-recipe="createNewRecipe"></new-recipe>
    <div v-for="recipe in recipeToShow" :key="recipe.recipeId">
      <recipe-item
        class="white"
        :recipe-details="recipe"
        @recipe-update="updateARecipe"
      ></recipe-item>
    </div>
  </div>
</template>

<script>
import RecipeItem from "./RecipeItem.vue";
import NewRecipe from "./NewRecipe.vue";

export default {
  name: "RecipeList",
  components: { NewRecipe, RecipeItem },
  props: {
    // msg: String
  },
  data() {
    return {
      recipes: [],
      filterBy: "all"
    };
  },
  mounted() {
    this.getFromLocalStorage();
  },
  methods: {
    createNewRecipe(_recipe) {
      // adds a new task to the array
      if (NewRecipe.recipeTitle.length > 0) {
        this.recipes.push(NewRecipe);
        this.saveToLocalStorage();
      }
    },
    updateARecipe(updatedRecipe) {
      this.recipes.forEach(recipe => {
        if (recipe.recipeId === updatedRecipe.itemId) {
          recipe.recipeTitle = updatedRecipe.itemTitle;
          recipe.recipeDescription = updatedRecipe.itemDesc;
          recipe.recipeStatus = updatedRecipe.itemStatus;
        }
      });
      this.saveToLocalStorage();
    },
    getFromLocalStorage() {
      if (localStorage.recipes) this.recipes = JSON.parse(localStorage.getItem("recipes"));
    },
    saveToLocalStorage() {
      localStorage.setItem("recipes",JSON.stringify(this.recipes));
    },
  },
  computed: {
    newRecipeId() {
      return (
        this.recipes.reduce((max, curr) => Math.max(max, curr.recipeId), 0) + 1
      );
    }
  }
};
</script>

<style scoped>
.white {
  background-color: rgb(255, 255, 255);
}
</style>