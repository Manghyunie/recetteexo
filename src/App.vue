<template>
  <div id="app">
    <div>RECIPES BOOK</div>
    <br>
    <recipe-list />
  </div>
</template>

<script>
import RecipeList from './components/RecipeList.vue';
export default {
  name: "app",
  components: {
    RecipeList
  }
};
</script>

<style>
#app {
  color: #665bff;
  margin-top: 5px;
  background-color: #ffffff;
}
</style>