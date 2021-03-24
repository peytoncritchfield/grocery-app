<template>
  <v-app>


    <div class="body">
      <div class="tabs">
        <div class="tabs__tab" :class="isActive === 0 ? 'tabs__tab' : 'unclicked'" @click="getRecipes()">
          Recipe List
        </div>
        <div class="tabs__tab" :class="isActive === 1 ? 'tabs__tab' : 'unclicked'" @click="getGroceries()">
          Grocery List
        </div>
      </div>


      <template v-if="templateMode === 0">
        <div class="simple-text">My Recipes</div>

        <div class="my-recipes" v-for="recipe in recipes" :key="recipe.id">
          {{ recipe.name }}
        </div>

        <div class="bottom-button-container">
          <div class="bottom-button" @click="newRecipe()">New Recipe</div>
        </div>
      </template>


      <template v-if="templateMode === 1">
        <div class="test">Hello Meghan</div>
      </template>


      <template v-if="templateMode === 2">
        <v-row>
          <v-text-field outlined label="Recipe Name" class="">

          </v-text-field>
        </v-row>
        <div class="bottom-button-container">
          <div class="bottom-button" @click="save()">Save</div>
        </div>
      </template>


    </div>
  </v-app>
</template>

<script>
import axios from "axios";

export default {
  name: "App",

  data() {
    return {
      isActive: 0,
      recipes: [],
      templateMode: 0,
    };
  },

  created() {
    this.getRecipes();
  },

  methods: {
    async getRecipes() {
      this.templateMode = 0;
      this.isActive = 0;
      let recipes = await axios.get(
        "http://localhost:5001/peytons-projects/us-central1/api/recipes"
      );
      this.recipes = recipes.data;
    },

    getGroceries() {
      this.templateMode = 1;
      this.isActive = 1;
    },

    async save() {
      this.templateMode = 0;
      this.isActive = 0;
      await axios.post(
        "http://localhost:5001/peytons-projects/us-central1/api/recipe",
        {
          name: "jakes new recipe",
        }
      );
      this.getRecipes();
    },

    newRecipe() {
      this.templateMode = 2;
      this.isActive = 2;
    },
  },
};
</script>

<style lang="scss">
.body {
  margin: 0px auto;
}

.tabs {
  justify-content: center;
  align-items: right;
  padding: 20px 40px;
  background-color: #eaebea;
  &__tab {
    display: inline-block;
    padding: 8px 16px;
    border-style: solid;
    border-width: 2px;
    border-color: #6e9361;
    border-radius: 25px;
    margin-right: 10px;
    background-color: #6e9361;
    color: white;
  }
}

.unclicked {
  background-color: #eaebea;
  color: #6e9361;
  &:hover {
    background-color: #6e9361;
    color: white;
    cursor: pointer;
  }
}

.simple-text {
  padding-top: 50px;
  padding-bottom: 25px;
}

.my-recipes {
  display: flex;
  background-color: #94768b;
  margin: 10px 10px;
  border-radius: 25px;
  height: 75px;
  align-items: center;
  padding-left: 20px;
  color: white;
}

.bottom-button-container {
  position: fixed;
  display: flex;
  align-items: center;
  justify-content: center;
  bottom: 0;
  background: linear-gradient(
    rgba(255, 255, 255, 0.925),
    rgba(255, 255, 255, 1)
  );
  width: 100%;
  left: 0;
  height: 20vh;
  max-height: 150px;
  min-height: 80px;
}

.bottom-button {
  margin: 10px 10px;
  display: flex;
  bottom: 20px;
  width: 315.16px;
  height: 75px;
  background: #ffffff;
  border: 3px solid #6e9361;
  border-radius: 25px;
  color: #6e9361;
  justify-content: center;
  align-items: center;

  &:hover {
    background-color: #6e9361;
    color: white;
    cursor: pointer;
  }
}

.test {
  color: black;
}
</style>