<script>
// Importacion de Axios para consumir API
import axios from 'axios'
export default{

  data(){
    return{
      paises:[]
    }
  },

  mounted(){
    //Se ejecuta al momento de montar el componente
      this.getAll()
  },

  methods:{

    getAll(){
      console.log('Mostrar Todos los Paises')
      axios.get('https://restcountries.com/v3.1/all')
      .then( response => {
        this.paises = response.data
        })
      .catch( e => console.log(e))
    },

    getRegion(region){
      console.log('Mostrar Paises por Region' + ' '+region)
      axios.get('https://restcountries.com/v3.1/region/' + region)
      .then( response => {
        this.paises = response.data
        })
      .catch( e => console.log(e))
    }
  }
}
</script>

<template>
  <div>

    <div class = 'menu'>
      <button v-on:click = 'getAll'>Any</button>
      <button v-on:click = 'getRegion("america")'>America</button>
      <button v-on:click = 'getRegion("africa")'>Africa</button>
      <button v-on:click = 'getRegion("europ")'>Europe</button>
      <button v-on:click = 'getRegion("oceania")'>Oceania</button>
      <button v-on:click = 'getRegion("asia")'>Asia</button>
    </div>

    <div class='contenedor-principal'>
      <div class= 'card' v-for="pais in paises" :key ="pais.id">
          <div  class= 'card-header'>
          <img v-bind:src= "pais.flags.png" class= 'pais-img'>
          </div>
          <div  class= 'card-body'>
            <strong><p>{{pais.name.common}}</p></strong>
            <p class='capital'>{{pais.capital?.toString()}}</p>
          </div>
      </div>
    </div>
  </div>
</template>


<style>
@import '../assets/css/styles.css'
</style>