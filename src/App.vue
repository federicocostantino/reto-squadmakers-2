<template>
  <v-app>

    <v-app-bar app dark class="header-bar">
      <h1>
        <v-img
          src="./assets/rick_and_morty.png"
          max-width="750"></v-img>
      </h1>
      <div class="buscador">
        <input type="text" placeholder="Buscar personaje...">
      </div>
    </v-app-bar>

    <v-toolbar class="vtoolbar">
      <template>
        <v-tabs
          v-model="tab"
          fixed-tabs
          background-color="#F4F8F8" 
          color="black" 
          slider-color="#42B928" 
          slider-size="3">
            <v-tab
              v-for="item in items"
              :key="item">
                {{item}}
            </v-tab>
        </v-tabs>
      </template>
    </v-toolbar>
    <v-tabs-items v-model="tab">
      <v-tab-item
        v-for="item in items"
        :key="item">
          <v-card>
            <v-card-text>
              <v-container class="container">
                  
                <header>
                  <p>Mostrar favoritos: <span>estrellita</span></p>
                </header>

                <main id="listado">
                  <div v-if="item == 'All'">
                    <div v-for="character in characters.results" :key="character">
                      <v-dialog
                        transition="dialog-top-transition"
                        max-width="780"
                      >
                        <template v-slot:activator="{ on, attrs }">
                            <v-card
                            v-bind="attrs"
                            v-on="on"
                            >
                              <div class="card__imagen">
                                <img v-bind:src="character.image" v-bind:alt="character.name">
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
                        </template>
                        <template v-slot:default="dialog">
                            <v-card>
                                <v-toolbar class="toolbar">
                                  <img v-bind:src="character.image" v-bind:alt="character.name">
                                  <div>
                                    <p> {{character.status}} </p>
                                    <p> {{character.name}} </p>
                                    <p> {{character.species}} </p>
                                  </div>
                                </v-toolbar>
                                
                                <v-card-text class="cardtext">
                                  <div>
                                    <div class="text-h3 py-6">Información</div>
                                    <div class="cardInformation">
                                      <div class="card_informacion">
                                        <p>Gender:</p>
                                        <p> {{character.gender}} </p>
                                      </div>
                                      <div class="card_informacion">
                                        <p>Origin:</p>
                                        <p> {{character.origin.name}} </p>
                                      </div>
                                      <div class="card_informacion">
                                        <p>Type:</p>
                                        <p v-if="character.type != ''"> {{character.type}} </p>
                                        <p v-else>Unknown</p>
                                      </div>
                                    </div>
                                  </div>

                                  <div>
                                    <div class="text-h3 py-6">Episodios</div>
                                    <div class="cardEpisodios">
                                      <div
                                        v-for="episode in episodes.results"
                                        :key="episode"  
                                      >
                                        <div 
                                          v-for="characterEpisode in episode.characters" 
                                          :key="characterEpisode"
                                          v-if="characterEpisode == character.url"  
                                        >
                                          <div class="card_episodios">
                                            <p> {{episode.name}} </p>
                                            <p> {{episode.episode}} </p>
                                            <p> {{episode.air_date}} </p>
                                          </div>
                                        </div>
                                      </div>
                                    </div>
                                  </div>

                                  <div>
                                    <div class="text-h3 py-6">Personajes interesantes</div>
                                    </div>
                                    
                                </v-card-text>

                                <v-card-actions class="justify-end">
                                    <v-btn
                                    class="btn-compartir"
                                    text
                                    @click="dialog.value = false"
                                    >Compartir personaje</v-btn>
                                </v-card-actions>
                            </v-card>
                        </template>
                      </v-dialog>
                    </div>
                  </div>

                  <div v-else>
                    <div v-for="character in characters.results" :key="character" v-if="character.gender == item">
                      <v-dialog
                        transition="dialog-top-transition"
                        max-width="780"
                      >
                        <template v-slot:activator="{ on, attrs }">
                            <v-card
                            v-bind="attrs"
                            v-on="on"
                            >
                              <div class="card__imagen">
                                <img v-bind:src="character.image" v-bind:alt="character.name">
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
                        </template>
                        <template v-slot:default="dialog">
                            <v-card>
                                <v-toolbar class="toolbar">
                                  <img v-bind:src="character.image" v-bind:alt="character.name">
                                  <div>
                                    <p> {{character.status}} </p>
                                    <p> {{character.name}} </p>
                                    <p> {{character.species}} </p>
                                  </div>
                                </v-toolbar>
                                
                                <v-card-text class="cardtext">
                                  <div>
                                    <div class="text-h3 py-6">Información</div>
                                    <div class="cardInformation">
                                      <div class="card_informacion">
                                        <p>Gender:</p>
                                        <p> {{character.gender}} </p>
                                      </div>
                                      <div class="card_informacion">
                                        <p>Origin:</p>
                                        <p> {{character.origin.name}} </p>
                                      </div>
                                      <div class="card_informacion">
                                        <p>Type:</p>
                                        <p v-if="character.type != ''"> {{character.type}} </p>
                                        <p v-else>Unknown</p>
                                      </div>
                                    </div>
                                  </div>

                                  <div>
                                    <div class="text-h3 py-6">Episodios</div>
                                    <div class="cardEpisodios">
                                      <div
                                        v-for="episode in episodes.results"
                                        :key="episode"  
                                      >
                                        <div 
                                          v-for="characterEpisode in episode.characters" 
                                          :key="characterEpisode"
                                          v-if="characterEpisode == character.url"  
                                        >
                                          <div class="card_episodios">
                                            <p> {{episode.name}} </p>
                                            <p> {{episode.episode}} </p>
                                            <p> {{episode.air_date}} </p>
                                          </div>
                                        </div>
                                      </div>
                                    </div>
                                  </div>

                                  <div>
                                    <div class="text-h3 py-6">Personajes interesantes</div>
                                    </div>
                                    
                                </v-card-text>

                                <v-card-actions class="justify-end">
                                    <v-btn
                                    class="btn-compartir"
                                    text
                                    @click="dialog.value = false"
                                    >Compartir personaje</v-btn>
                                </v-card-actions>
                            </v-card>
                        </template>
                      </v-dialog>
                    </div>
                  </div>

                </main>
              </v-container>
            </v-card-text>
          </v-card>
      </v-tab-item>
    </v-tabs-items>
  </v-app>
</template>

<script>

import axios from 'axios'

export default {
  name: 'App',
  components: {
  },

  data: () => ({
    tab: null,
    items: ['All','unknown','Female','Male','Genderless'],
    characters: [],
    episodes: [],
  }),

  mounted() {
      this.getTodos();
      this.getEpisodios();
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

      getEpisodios() {
        axios.get('https://rickandmortyapi.com/api/episode')
        .then(response => {
            console.log(response);
          this.episodes = response.data;
        }).catch(e => {
          console.error("Error: " + e);
        })
      }
    },
};
</script>

<style>

  .header-bar {
    width: 100% !important;
    min-height: 600px !important;
    max-height: 600px !important;
    position: relative !important;
    background-image: url("./assets/banner.jpg");
    background-position: center;
    background-size: cover;
    position: relative;
    display: flex !important;
    justify-content: center;
  }

  .header-bar .v-toolbar__content {
    flex-direction: column;
  }

  .header-bar:before {
    content:'';
    position: absolute;
    top: 0;
    bottom: 0;
    left: 0;
    right: 0;
    background-color: rgba(0,0,0,0.6);
  }

  .buscador {
    margin-top: 50px;
    
    color: white !important;
  }

  .buscador input {
    padding: 30px 100px 30px 50px;
    background-color: #2C3157;
    border: 1px solid white;
    color: white;
    font-size: 1.25em;
  }

  .v-application--wrap {
    min-height: none !important;
  }

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
    width: 100%;
    display: flex;
  }

  .container > main > div {
    width: 100%;
    display: flex;
    flex-wrap: wrap;
    justify-content: space-between;
  }
  .container > main > div > div {
    width: 30%;
    height: 300px;
  }

  .container > main > div > div .v-card {
    width: 100%;
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

  .container main div .v-card .card__info .card__title,
  .toolbar .v-toolbar__content div p:nth-child(2){
    font-size: 1.5em;
    font-weight: bold;
  }

  .toolbar {
    height: auto !important;
  }

  .toolbar .v-toolbar__content {
    height: auto !important;
    padding: 15px;
    text-align: center;
    flex-direction: column !important;
  }

  .cardtext {
  }

  .cardInformation {
    display: flex;
    justify-content: space-between;
  }

  .cardEpisodios {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-between;
  }

  .cardEpisodios div {
    width: 30%;
  }

  .cardEpisodios > div > div {
    width: 100%;
    border: 1px solid lightgray;
    margin-bottom: 20px;
    padding: 10px;
  }

  .cardEpisodios > div > div > .card_episodios {
    width: 100%;
  }

  .cardEpisodios > div > div > .card_episodios p:first-child {
    margin-bottom: 0;
  }

  .card_informacion {
    width: 30%;
    padding: 10px;
    border: 1px solid lightgray;
    display: flex;
    flex-direction: column;
  }

  .card_informacion p:first-child,
  .cardEpisodios > div .card_episodios p:nth-child(2) {
    margin-bottom: 0;
  }

  .card_informacion p:last-child,
  .cardEpisodios > div .card_episodios p:nth-child(2) {
    font-size: 1.2em;
    font-weight: bold;
  }

  .btn-compartir {
    padding: 40px !important;
    border-radius: 45px !important;
    background-color: #266668;
    color: white !important;
    font-size: 1.25em !important;
  }
  

</style>
