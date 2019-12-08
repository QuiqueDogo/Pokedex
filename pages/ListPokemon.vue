<template>
    <div class="container-pok">
    <div class="list">
        <IndividualPokemon 
        v-for="(element, index) in pokemonSave"
        :key="index"
        v-on:click.native="GetInfo(element.url)"
        :name="element.name"
        :img="element.img"
        />
    </div>
    <div class="detail">
        <button class="pokemon">Liberar Pokemons</button>
        <detail :info="info" :sprites="sprites" :allsprites="allsprites"/>
    </div>
    <audio autoplay loop :src="require('~/static/PokemonCenter.mp3')" />
    </div>
</template>

<script>
import IndividualPokemon from "~/components/IndividualPokemon.vue"
import Detail from "~/components/Detail.vue"

export default {
    components:{
        IndividualPokemon,
        Detail
    },
    data(){
        return {
            pokemonSave:[],
            info:"",
            sprites:"",
            allsprites:[]
        }
    },
    mounted(){
        this.getLocalStorage();
        
    },

    methods:{
        getLocalStorage(){
                const PokemontoPrint = localStorage.getItem('pokemonList');
                if(PokemontoPrint !== null ){
                    this.pokemonSave = JSON.parse(PokemontoPrint);
                }
        },
        GetInfo(url){
            this.$axios.get(url)
            .then(response => {
                this.info = response.data,
                this.sprites = response.data.sprites.front_default
                // this.allsprites = response.data.sprites
                this.getSprites(response.data.sprites);
            })
            .catch(e => console.log(e));
        },
        clearLocalStorage(){
            localStorage.removeItem('pokemonList');
            this.$toasted.show(`Pokemons Liberados`,{type:'success',duration:2000})
        },
        getSprites(sprites){
            var Allsprites = [];
            for(const prop in sprites){
                if (sprites[prop] !== null) {
                    Allsprites.push(sprites[prop]);
                }
            }
            this.allsprites = Allsprites;
        }
    },
}
</script>

<style >
*{
    font-family: 'Open Sans', cursive;
}

.list{
    flex: 0.35;
}

.detail{
    flex: 1;
}

.image{
    width: 100%;
    height: 70%;
    border-bottom: 1px solid white;
    border-color: white;
    display: flex;
    align-items: center;
    justify-content: center;
}
.text{
    margin: auto 0;
    color: black;
    text-transform: capitalize;
}
.container-pok{
    height: 90vh;
    width: 90%;
    margin:30px auto; 
    display: flex;
}

.pokemon{    
    position: absolute;
    right: 5%;
    background: #f8f8f8;
    border-radius: 10px;
    border: 0;
    height: 30px;
    background: rgba(238, 75, 75, 0.89);
    color:white;
}
</style>