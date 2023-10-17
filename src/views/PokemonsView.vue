<template>
    <div class="container">
        <div class="row d-flex justify-content-center">
            <div v-for="pokemon in pokemons" :key="pokemon.name" class="col-sm-4 mt-3 pt-3 pb-3">
                <router-link :to="{name:'pokemon-detail',params:{name:pokemon.name}}">
                    <div class="card p-3 d-flex align-items-center">
                        <div class="card-title">
                            <h3 class="text-center">
                                {{ pokemon.name }}
                            </h3>
                        </div>
                    </div>
                </router-link>
            </div>
        </div>
    </div>
</template>
<script>
import PokemosService from '@/services/PokemonServices'
export default {
    name: 'PokemonsView',
    data(){
        return {
            pokemons: []
        }
    },
    async created() {
        this.pokemons = await PokemosService.getPokemons()
        console.log(this.pokemons)
    }
}
</script>