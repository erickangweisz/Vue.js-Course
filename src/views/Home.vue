<template>
  <div>
    <v-container>
      <h1 class="text-center">Pokemon-Picker</h1>
      <br>
      <v-row justify="center">
        <v-flex lg4 md5 sm7 justify="center">
          <v-card
            class="mx-auto"
            color="#385F73"
            dark
            outlined>

            <v-btn block color="warning" dark @click="getPokemon('pikachu')">
              <i class="material-icons">flash_on</i> Pikachu
            </v-btn>
            <v-btn block color="primary" dark @click="getPokemon('charmander')">
              <i class="material-icons">whatshot</i> Charmander</v-btn>
            <v-btn block color="success" dark @click="getPokemon('bulbasaur')">
              <i class="material-icons">spa</i> Bulbasaur
            </v-btn>

            <v-list-item three-line>
              <v-list-item-content>
                <div class="overline mb-4">Base experience: {{ base_experience }}</div>
                <div class="overline mb-4">Order: {{ order }}</div>
                <v-list-item-title class="headline mb-1">{{ pokemon_name }}</v-list-item-title>
              </v-list-item-content>

              <v-list-item-avatar
                size="90"
                color="white">
                <v-img :src="front_default_sprite"/>
              </v-list-item-avatar>
            </v-list-item>

          </v-card>
        </v-flex>
      </v-row>
    </v-container>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  data () {
    return {
      pokemon_name: 'select a pokemon',
      base_experience: '',
      front_default_sprite: '',
      order: ''
    }
  },
  methods: {
    async getPokemon(pokemonName) {
      let data = await axios.get(`https://pokeapi.co/api/v2/pokemon/${pokemonName}`)
     
      this.pokemon_name = data['data'].name
      this.base_experience = data['data'].base_experience
      this.front_default_sprite = data['data'].sprites['front_default']
      this.order = data['data'].order
    }
  }
}
</script>
