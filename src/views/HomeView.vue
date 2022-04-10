<template>
  <div>
    <input
      type="text"
      name="search"
      id="search"
      placeholder="search cocktail"
      v-model="cocktail"
    />
    <button @click="cocktailreceipe">search</button>
  </div>
  <div class="maincontainer">
    <div
      class="bigcontainer"
      v-for="(element, index) in cocktails"
      :key="index"
    >
      <div><img :src="element.strDrinkThumb" /></div>
      <br />
      <div class="textcontainer">
        <strong>Cocktail name:</strong> {{ element.strDrink }}<br />
        <br />
        <strong>Instructions:</strong> {{ element.strInstructions }}<br /><br />
        <strong>Ingredients:</strong>
        <ul>
          <li>{{ element.strIngredient1 }}</li>
          <li>{{ element.strIngredient2 }}</li>
          <li>{{ element.strIngredient3 }}</li>
          <li>{{ element.strIngredient4 }}</li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
const Home = {
  data() {
    return {
      cocktails: [],
      cocktail: "",
    };
  },

  async mounted() {
    let receipe = await fetch(
      "https://www.thecocktaildb.com/api/json/v1/1/search.php?s="
    );
    let data = await receipe.json();
    console.log(data);
    this.cocktails = data.drinks;
  },

  methods: {
    async cocktailreceipe() {
      const cocktaildetail = await fetch(
        "https://www.thecocktaildb.com/api/json/v1/1/search.php?s=" +
          this.cocktail
      );

      let myreceipes = await cocktaildetail.json();
      console.log(myreceipes, "cocktail");
      this.cocktails = myreceipes.drinks;
    },
  },
};

export default Home;
</script>

<style scoped>
img {
  max-width: 50%;
}
.maincontainer {
  display: flex;
  flex-wrap: wrap;
}
.bigcontainer {
  display: flex;
  flex-direction: row;
  padding: 50px;
  border-bottom: black solid 2px;
  max-width: 50%;
  max-height: 50%;
  margin-right: auto;
  margin-left: auto;
}

.textcontainer {
  max-width: 70%;
  text-align: left;
}
</style>
