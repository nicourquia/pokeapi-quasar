<template>
  <q-page class="flex flex-center">
      <q-card v-for="poke in pokemons" :key="poke.id" class="my-card">
      <img :src="poke.url">

      <q-card-section>
        <div class="text-h6">{{poke.name}}</div>
        <div class="text-subtitle2">Tipo: {{poke.type}}</div>
      </q-card-section>
    </q-card>
  </q-page>
</template>

<script>
//import { createDOMCompilerError } from '@vue/compiler-dom';
import { defineComponent } from 'vue'
import axios from "axios";

export default defineComponent({
  name: 'IndexPage',
  setup (){
    return{
      pokemons: [],
    }
  },
  created() {
    this.getPokemons();
    
  },
  mounted(){
  },
  methods: {
    getPokemons(){
      for(let i = 0; i <= 9; i++){
        axios.get(`https://pokeapi.co/api/v2/pokemon/${i+1}`).then((result) => {
          let pokemon = {
            name: result.data.name,
            url: result.data.sprites.front_default,
            type: result.data.types[0].type.name,
          }
          this.pokemons.push(pokemon)
        })
        .catch((e) => console.log(e))
      }
    }
  }
})
</script>

<style lang="sass" scoped>
.my-card
  width: 100%
  max-width: 250px
</style>
