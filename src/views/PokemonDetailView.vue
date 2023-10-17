<template>
    <div class="container">
        <div class="row d-flex justify-content-center">
            <div  class="col-sm-8 mt-3 pt-3 pb-3">
                <div class="card">
                    <div class="card-title">
                        <h3 class="text-center">
                            {{ pokemon.name }}
                        </h3>
                    </div>
                    <div class="card-body">
                        <img v-if="image" :src="image" alt="" width="200" height="200">
                        <div class="d-flex aligm-items-bottom">
                            <p> <stong>Tipo: </stong></p>
                            <p style="margin-right: 5px; margin-left: 2px;" v-for="(type, index) in types" :key="index">
                                {{ type.type.name }}
                            </p>
                        </div>
                        <div class="d-flex">
                            <button @click="goToStats()" class="btn btn-primary m-3">
                                Ver Estadísticas
                            </button>
                            <button @click="goToAbilities()" class="btn btn-warning m-3">
                                Ver habilidades
                            </button>
                            <button @click="goToMoves()" class="btn btn-success m-3">
                                Ver movimientos
                            </button>
                        </div>
                    </div>
                </div>
            </div>
        </div>
        <div class="row d-flex justify-content-center">
            <div  class="col-sm-8 mt-3 pt-3 pb-3">
                <router-view></router-view>
            </div>
        </div>
    </div>
</template>
<script>
import { useRoute } from 'vue-router'
import PokemonService from '@/services/PokemonServices'
export default {
    name: 'PokemonDetail',
    data(){
        return {
            name:'',
            pokemon: {},
            types: [],
            image: null,
            
        }
    },
    async created() {
        const route = useRoute()
        this.name = route.params.name
        this.pokemon = await PokemonService.getPokemonDetail(this.name)
        this.types = this.pokemon.types
        this.image = this.pokemon.sprites.other.dream_world.front_default
    },
    methods: {
        goToStats() {
            this.$router.push({
                name:'stats'
            })
        },
        goToAbilities() {
            this.$router.push({
                name:'abilities'
            })
        },
        goToMoves() {
            this.$router.push({
                name:'moves'
            })
        }
    }
}
</script>


