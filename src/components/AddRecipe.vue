<template>
    <h1>Recipe Book</h1>
    <div id="app">

        <form @submit.prevent action="submit">
            <input type="text" v-model="recipeName" placeholder="Add new recipe">
            <button @click="addRecipe">Add Recipe</button>
        </form>
        <ul>
            <li v-for="(recipe, index) in recipes" :key="index">
                {{ recipe.recipeName }}
                <button @click="toggleEdit(recipe, index)">Edit</button>
                <button @click="clearOne(index)">Delete</button>
            </li>
        </ul>
    </div>

    <div id="edit" v-if="isEditing">
        <h1>Edit your recipe</h1>
        <input v-model="editRecipe.recipeName">
        <textarea name="" id="" cols="50" rows="10" v-model="editRecipe.recipeDescription">
        </textarea>
        <ul>
            <li v-for="ingredient in editRecipe.recipeIngredients" >
                <p>{{ ingredient.name }}</p>
                <button>Delete</button>
            </li>
        </ul>
        <form @submit.prevent action="submit">
            <input type="text" v-model="recipeIngredients" placeholder="Add new ingredient">
            <button @click="addIngredient(recipe)">Add Ingredient</button>
        </form>
        <button @click="saveEdit()">Save</button>
        <button @click="">Add to shopping list</button>

    </div>
    
</template>

<script>

export default{
    name: 'AddRecipe',
    
  data () {
    return {
        recipes: [{
            recipeName: 'boeuf bourguignon',
            recipeDescription: 'pour 4',
            uuid: 0,
            recipeIngredients: [{
                name: 'boeuf',
                uuid: 0
            }],
        }],

        editRecipe: {
            recipeName: 'edition',
            recipeDescription: 'edition',
            uuid: 0,
            recipeIngredients: ["edition"],
        },


        recipeName: '',
        recipeDescription: 'description par default',
        uuid: 0,
        recipeIngredients: [],
        isEditing: false,
    }
  },
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


    toggleEdit(recipe, index){
        this.isEditing = true;

        this.editRecipe = recipe
        this.clearOne(index)
        console.log(recipe.uuid) 
    },

    // addIngredient(recipe){
    //     console.log(this.recipes[recipe.uuid])
    // }
    
    saveEdit(){
        this.recipes.push(this.editRecipe)
        this.isEditing = false;

    }

  }
}
</script>
