<template>
  <v-container class="container">
    
    <header>
      <p>Mostrar favoritos: <span>estrellita</span></p>
    </header>

    <main id="listado">
      <div v-for="character in characters.results" :key="character">
        <v-card>
          <div class="card__imagen">
            <img v-bind:src="character.image" alt="">
          </div>
          <div class="card__info">

            <div>
              <p> {{character.status}} - {{character.species}} </p>
            </div>

            <div class="card__title">
              <p> {{character.name}} </p>
            </div>

            <div>
              <p>Last know location:</p>
              <p> {{character.location.name}} </p>
            </div>

            <div>
              <p>First seen in:</p>
              <p> {{character.origin.name}} </p>
            </div>

          </div>
        </v-card>
      </div>
    </main>
    
  </v-container>
</template>

<style>

  .container {
    width: 100%;
  }

  .container header {
    height: 100px;
    display: flex;
    align-items: center;
  }

  .container header p {
    font-size: 2em;
  }

  .container main {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-between;
  }

  .container > main > div  {
    width: 30%;
  }

  .container main div .v-card {
    width: 100%;
    height: 300px;
    border: 1px solid lightgrey;
    margin-bottom: 3em;
    display: flex;
  }

  .container main div .v-card .card__imagen{
    width: 40%;
  }

  .container main div .v-card .card__imagen img{
    width: 100%;
    height: 100%;
  }

  .container main div .v-card .card__info{
    width: 60%;
    margin-left: 20px;
    padding: 10px 0;
  }

  .container main div .v-card .card__info .card__title{
    font-size: 2em;
  }

</style>

<script>

  import axios from 'axios';

  export default {
    name: 'All',

    data: () => ({
      characters: [],
    }),

    mounted() {
      this.getTodos();
    },

    methods: {
      getTodos() {
        axios.get('https://rickandmortyapi.com/api/character')
        .then(response => {
            console.log(response);
          this.characters = response.data;
        }).catch(e => {
          console.error("Error: " + e);
        })
      },
    },
  }
</script>