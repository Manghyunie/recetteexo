<template>
    <div>
      <div>
        <div>
          <div class="clickable" @click="showDescription = !showDescription">
            <input
              class="clickable"
              :disabled="!editTitle"
              type="text"
              v-model="recipe.itemTitle"
              @blur.stop="editTitle = false"
            />
          </div>
          <button v-show="!showDescription" @click="editTitle = !editTitle">
            {{ editTitleButton }}
          </button>
        </div>
      </div>
      <div v-show="showDescription">
        <textarea
          :disabled="!editDescription"
          v-model="recipe.itemDesc"
          @blur.stop="editDescription = false"
        ></textarea>
      </div>
      {{ recipe.itemStatus }}
      <button
        v-show="showDescription"
        @click="editDescription = !editDescription"
      >
        {{ editDescriptionButton }}
      </button>
      <button @click="moveToDeleted">Delete</button>
    </div>
  </template>
  
  <script>
  export default {
    name: "RecipeItem",
    props: {
      RecipeDetails: {
        recipeTitle: String,
        recipeDescription: String,
        recipeStatus: String,
        recipeId: Number
      }
    },
    data() {
      return {
        showDescription: false,
        editDescription: false,
        editTitle: false,
        recipe: {
          itemTitle: this.recipeDetails.recipeTitle,
          itemDesc: this.recipeDetails.recipeDescription,
          itemStatus: this.recipeDetails.taskStatus,
          itemId: this.recipeDetails.recipeId
        }
      };
    },
    methods: {
      moveToDeleted() {
        this.recipe.itemStatus = "deleted";
      }
    },
    updated() {
      this.$emit("recipe-update", this.recipe);
    },
    computed: {
      editTitleButton() {
        return this.editTitle ? "save" : "edit";
      },
      editDescriptionButton() {
        return this.editDescription ? "save" : "edit";
      },
    }
  };
  </script>
  
  <style scoped>
  .clickable {
    cursor: pointer;
  }
  .todo {
    text: rgb(255, 255, 255);
  }
  </style>