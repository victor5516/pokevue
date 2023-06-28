<template>
<header class="header">
  <label>
    Nombre o ID
    <input type="text"
    placeholder="Buscar pokemon"
    v-model="pokemonID"

    />
  </label>
  <button
  @click="searchPokemon"
  >Buscar</button>
</header>
<main
v-if="Object.keys(pokemonData).length > 0"
>
  <section class="pokemonCard">
    <div>
      <h1>{{ pokemonData.name }}</h1>
      <img :src="pokemonData.sprites.front_default"
      :alt ="pokemonData.name" />
    </div>
    <ul>
      <h2>Tipo:</h2>
      <li v-for="(type, index) in pokemonData.types" :key="index"
      >
        <span> {{ type.type.name }} </span>
    </li>
    </ul>
    <ul>
      <h2>Estadisticas</h2>
      <li v-for="(stat, index) in pokemonData.stats" :key="index">
        <span> {{ stat.stat.name }} -> {{ stat.base_stat }}</span>
      </li>
    </ul>
  </section>
</main>
</template>

<script>

import { pokeApi } from '@/api/pokeApi'
export default {

  name: 'App',
  data(){
    return {
      pokemonData: {},
      pokemonID: ''
    }
  },
  methods: {
    async searchPokemon () {
      try{
         const response = await fetch(`${pokeApi}/${this.pokemonID}`)
         const data = await response.json()
         this.pokemonData = data
         console.log(data)
         return data
      } catch (error) {
        console.log(error)
        alert('Pokemon no encontrado')
      }
    }
  }

}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  color: #2c3e50;
}
</style>
@/api/pokeApi