<template>
  <div id="app">
    
    <header>
      <div class="logo">
        <img src="./assets/img/logo.png" alt="logo spotify">
        <select v-model="selected" v-on:click="genre_selected">
          <option disabled value="">Please Select</option>
          <option v-for="disco in dischi" :key="disco.poster"> {{disco.genre}} </option>
        </select>
      </div>
    </header>
    <main>
      <div class="container">
        <div class="card" v-for="disco in dischi" :key="disco.poster">
          <img :src="disco.poster" alt="immagine album">
          <h2> {{disco.title}} </h2>
          <p> {{disco.author}} </p>
          <p> {{disco.year}} </p>
        </div>
      </div>
    </main>


  </div>
</template>

<script>
import axios from 'axios';

export default {
  name: 'App',
  components: {

  },
  data() {
    return {
      dischi: null,
      selected: '',
      genres: [],
      selected_dischi: []
    }
  },
  methods: {
    genre_selected(){
      this.dischi.forEach(disco => {
        if(disco.genre === this.selected){
        this.selected_dischi.push(disco)
      }
      });
    }
  },
  mounted() {
    axios
    .get('http://localhost/PHP/esercizi-php/php-ajax-dischi/')
    .then(response => {
      console.log(response.data);
      this.dischi = response.data;
    })
    .catch(err => {
      console.error(err);
    })
  }
}
</script>

<style lang="scss">
*{
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }
#app {
    header{
      background-color: #2e3a46;
    }
    .logo{
      display: flex;
      align-items: center;
      justify-content: space-between;
    }
    .logo img{
      height:100px;
      padding: 10px;
    }
    .logo > select{
      margin-right: 3rem;
      padding: 1rem;
      border-radius: 10px;
      border: none;
    }
    main{
      background-color: #1e2d3b;
      height: calc(100vh - 100px);
    }
    .container{
      max-width: 1440px;
      display: flex;
      margin: 0 auto;
      padding-top: 4rem;
      column-gap: 2rem;
      row-gap: 1rem;
      flex-wrap: wrap;
    }
    .card{
      width: calc(100% / 5 - 2rem);
      background-color: #2e3a46;
      display: flex;
      align-items: center;
      flex-direction: column;
      padding-bottom: 1rem;
    }
    .card > img{
      max-width: calc(100% - 1rem);
      padding: 1rem;
    }
    .card > h2{
      color: white;
      padding: 1rem;
      text-align: center;
    }
    .card > p{
      color: grey;
    }
}
</style>
