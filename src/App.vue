<template>
  <h1>personagens</h1>
  <div>
    <input type="text" v-model="searchName">
    <button @click="search">Pesquisar</button>
  </div>
  <div v-for="character in characters" :key="character.id" class="card">
    <img :src="character.image" alt="" class="character-image">
    <div class="character-info">
      <h3>{{character.name}}</h3>
      <p>{{character.gender}} | {{character.species}}</p>
    </div>
    <button>Detalhes</button>
  </div>
</template>

<script>
import api from './services/api'

export default {
  components: {  },
  data() {
    return {
      searchName: "",
      characters: []
    }
  },
  mounted() {
    api.get('/character').then(response => {
      this.characters = response.data.results
      console.log(response.data.results)
    })
  },
  methods: {
    search() {
      api.get(`/character?name=${this.searchName}`).then(response => {
        this.characters = response.data.results
        console.log(response.data.results)
      })
    }
  }
}  
</script>

<style scoped>
  .card {
    background: white;
    height: 18rem;
    width: 20rem;
    box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2);
    transition: 0.3s;
    border-radius: 4px;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: space-between;
    padding: 1rem;
    margin: 0.5rem 0.5rem
  }
  .card:hover {
    box-shadow: 0 8px 16px 0 rgba(0,0,0,0.2);
  }
  .character-image {
    width: 18rem;
    height: 12rem;
    border-radius: 0.25rem;
  }
  .character-info {
    display: flex;
    flex-direction: column;
    align-items: center;
  }
</style>
