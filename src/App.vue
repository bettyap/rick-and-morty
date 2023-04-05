<template>
  <h1>personagens</h1>
  <div>
    <input type="text" v-model="searchName">
    <button @click="search">Pesquisar</button>
  </div>
  <ul>
    <li v-for="character in characters" :key="character.id">
      {{character.name}}
      <img :src="character.image" alt="" >
    </li>
  </ul>
</template>

<script>
import api from './services/api'

export default {
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

</style>
