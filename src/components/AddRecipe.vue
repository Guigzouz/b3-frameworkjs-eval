<template>

<!-- bloc input pour ajouter de nouvelles recettes de façon sommaire -->
    <div id="app">
            <h1>Recipe Book</h1>

            <form @submit.prevent action="submit">
                <input type="text" v-model="recipeName" placeholder="Add new recipe">
                <button @click="addRecipe">Add Recipe</button>
            </form>

        <ol>
            <li v-for="(recipe, index) in recipes" :key="index">
                {{ recipe.recipeName }}
                <button @click="toggleEdit(recipe, index)">Edit</button>
                <button @click="clearOne(index)">Delete</button>
            </li>
        </ol>

    </div>


<!-- bloc edition qui est affiché au clic de bouton edit -->

    <div id="edit" v-if="isEditing" style="display: flex; flex-direction: column;">
        <h1>Edit your recipe</h1>

        <input v-model="editRecipe.recipeName">
        <textarea name="" id="" cols="50" rows="10" v-model="editRecipe.recipeDescription"></textarea>
        
        <h2>Ingredients</h2>
        <ol>
            <li v-for="(ingredient, index) of editRecipe.recipeIngredients" :key="index" >
                {{ ingredient }}<button @click="clearOneIngredient(index)">Delete</button>
            </li>
        </ol>

        <form @submit.prevent action="submit">
            <input type="text" v-model="newRecipeIngredient" placeholder="Add new ingredient">
            <button type="button" @click="addIngredient()">Add Ingredient</button>
        </form>

        <button @click="saveEdit()">Save</button>
    </div>
</template>

<script>

export default{
    name: 'AddRecipe',
    
  data () {
    return {
        newRecipeIngredient: '',
        recipes: [{
            recipeName: 'boeuf bourguignon',
            recipeDescription: 'pour 4',
            uuid: 0,
            recipeIngredients: [
                "boeuf",
                "vin",
                "machette haitienne",
            ],
        }],

        editRecipe: {
            recipeName: 'edition',
            recipeDescription: 'edition',
            uuid: 0,
            recipeIngredients: ['edition'],
        },


        recipeName: '',
        recipeDescription: 'description par default',
        uuid: 0,
        recipeIngredients: [],
        isEditing: false,
    }
  },

//   fonction qui sont utilisées dans la page

  methods: {
    addRecipe() {
      this.recipes.push({
          recipeName: this.recipeName,
          recipeDescription: '',
          uuid: this.uuid++,
          recipeIngredients: this.recipeIngredients

      });
    },

    clearOne(index){
        this.recipes.splice(index, 1)
    },

    clearOneIngredient(index){
        this.editRecipe.recipeIngredients.splice(index, 1)
    },

    toggleEdit(recipe, index){
        this.isEditing = true;

        this.editRecipe = recipe
        this.clearOne(index)
        console.log(recipe.uuid) 
    },

    addIngredient(){
        this.editRecipe.recipeIngredients.push(this.newRecipeIngredient)
    },
    
    saveEdit(){
        this.recipes.push(this.editRecipe)
        this.isEditing = false;

    }

  }
}
</script>
