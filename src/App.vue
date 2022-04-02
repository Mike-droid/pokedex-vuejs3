<template>
  <header>
    <label for="pokemonInput">
      Type pokemon name or ID:
      <input
        type="text"
        id="pokemonInput"
        v-model="pokemonID"
      >
    </label>
    <button
      @click="searchPokemon"
    >
      Search pokemon!
    </button>
  </header>

  <main v-if="Object.entries(pokemonData).length > 0">
    <h1>{{ pokemonData.name }}</h1>
    <img
      :src="pokemonData.sprites.front_default"
      :alt="pokemonData.name"
    >
    <ul class="type">
      <li
        v-for="(type, key) in pokemonData.types"
        :key="key"
        :class="type.type.name"
      >
        <span>{{ type.type.name }}</span>
      </li>
    </ul>
    <ul class="stats">
      <h2>Stats:</h2>
      <li
        v-for="(stat, key) in pokemonData.stats"
        :key="key"
      >
        <span>{{ stat.stat.name}} -> {{stat.base_stat }}</span>
      </li>
    </ul>
  </main>
</template>

<script>
import { pokeapi } from '@/api/pokeapi'

export default {
  name: 'App',
  data () {
    return {
      pokemonData: {},
      pokemonID: '',
    }
  },

  methods: {
    async searchPokemon () {
      try {
        const pokemonToFind = await fetch(`${pokeapi}/${this.pokemonID}`)
        const pokemon = await pokemonToFind.json()
        this.pokemonData = pokemon
        console.log(pokemon)
        return pokemon
      } catch (error) {
        alert('Pokemon was not found')
      }
    }
  }
}
</script>

<style lang="scss" scoped>
@import './pokemon_types.scss';
@import url('https://fonts.googleapis.com/css2?family=Changa:wght@400;700&display=swap');

header, main, input[type="text"], button {
  font-family: 'Changa', sans-serif;
}

ul {
  padding: 0;
}

.type {
  & li {
    list-style: none;
    color: white;
    text-transform: uppercase;
  }
}

.stats {
  color: black;
}


.normal {
  background-color: $normal
}
.fire {
  background-color: $fire
}
.water {
  background-color: $water
}
.grass {
  background-color: $grass
}
.electric {
  background-color: $electric
}
.ice {
  background-color: $ice
}
.fighting {
  background-color: $fighting
}
.poison {
  background-color: $poison
}
.ground {
  background-color: $ground
}
.flying {
  background-color: $flying
}
.psychic {
  background-color: $psychic
}
.bug {
  background-color: $bug
}
.rock {
  background-color: $rock
}
.ghost {
  background-color: $ghost
}
.dark {
  background-color: $dark
}
.dragon {
  background-color: $dragon
}
.steel {
  background-color: $steel
}
.fairy {
  background-color: $fairy
}
</style>