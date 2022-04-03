<template>
  <header class="header">
    <label for="pokemonInput">
      Type pokemon name or ID:
      <input
        type="text"
        id="pokemonInput"
        v-model="pokemonID"
      >
    </label>
    <button
      class="searchButton"
      @click="searchPokemon"
    >
      Search pokemon!
    </button>
  </header>

  <main
    class="main"
    v-if="Object.entries(pokemonData).length > 0"
  >
    <section class="pokemonCard">
      <div class="nameImage">
        <h1 class="pokemonName">{{ pokemonData.name }}</h1>
        <img
          :src="pokemonData.sprites.front_default"
          :alt="pokemonData.name"
        >
      </div>
      <ul class="type">
        <h2>Type:</h2>
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
    </section>
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

.header, .main, input[type="text"], .searchButton {
  font-family: 'Changa', sans-serif;
}

.header, input[type="text"], .searchButton {
  font-size: 1.5rem;
}

.main {
  font-size: 1.2rem;
  background-color: $pokedex-green;
}

.header {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100px;
  background-color: $pokedex-red;
  color: white;

  & .searchButton {
  background-color: #1cb02b;
  color: white;
  border: none;
  margin-left: 10px;
  border-radius: 10px;
  cursor: pointer;

  &:hover {
    background-color: #1c8b0a;
  }
}

  & input[type="text"] {
    border-radius: 10px;
    outline: none;
    border: none;
  }
}


.pokemonCard {
  display: flex;
  flex-direction: row;
  justify-content: space-around;
  align-content: center;

  & .nameImage, & .type, & .stats {
    width: 33%;
    display: flex;
    flex-direction: column;
    justify-content: flex-start;
    align-items: center;
  }

  & .nameImage {
    & .pokemonName {
      text-transform: capitalize;
    }

    & img {
      width: 200px;
      background-color: $pokedex-blue;
      border-radius: 50%;
    }
  }

  & .type li {
    width: 90%;
    margin-bottom: 10px;
    text-align: center;
    border-radius: 20px;
  }

  & .stats li {
    align-self: flex-start;
  }
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

  & li {
    list-style: none;
    text-transform: uppercase;
  }
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

@media screen and (max-width: 820px) {

  .header {
    flex-direction: column;
    height: 120px;

    & .searchButton {
      width: 70%;
      margin-top: 10px;
    }
  }
  .pokemonCard {
    flex-direction: column;
    align-items: center;
  }
}

@media screen and (max-width: 600px) {
  .header {
    font-size: 1rem;

    & input[type="text"] {
      font-size: 1rem;
    }

    & .searchButton {
      font-size: 1rem;
    }
  }

  .pokemonCard {
    & .stats {
      width: 90%;
    }
  }
}

@media screen and (max-width: 400px) {
  .header {
    & label {
      text-align: center;
    }
  }
}
</style>