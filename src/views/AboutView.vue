<template>
  <div>
    <form @submit.prevent="fetchCocktail">
      <label for="cocktailName">Cocktail Name:</label>
      <input type="text" id="cocktailName" v-model="name" required />
      <button type="submit">Recherche</button>
    </form>

    <div v-if="cocktailData">
      <h2>Cocktail Data:</h2>
      <pre>{{ cocktailData }}</pre>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
import config from '/config.js'; 

export default {
  data() {
    return {
      cocktailData: null,
      name: '',
      apiKey: config.apiKey,
    };
  },
  methods: {
    fetchCocktail() {
      axios.get('https://api.api-ninjas.com/v1/cocktail', {
        params: {
          name: this.name,
        },
        headers: {
          'X-Api-Key': this.apiKey,
        },
      })
      .then(response => {
        this.cocktailData = response.data;
      })
      .catch(error => {
        console.error('Error fetching cocktail data', error);
      });
    },
  },
};
</script>

<style>
</style>
