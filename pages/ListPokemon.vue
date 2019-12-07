<template>
    <div class="container-pok">
    <img style="position:absolute;bottom:0;right:0; width:400px; heigth:400px;" src="https://i.imgur.com/YWy6sdr.png" alt="" srcset="">
    <div class="list">
        <p style="text-align:center;">Mis Pokemons</p>
        <IndividualPokemon 
        v-for="(element, index) in pokemonSave"
        :key="index"
        v-on:click.native="GetInfo(element.url)"
        :name="element.name"
        :img="element.img"
        />
    </div>
    <div class="detail">
        <detail />
    </div>
    
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
            pokemonSave:[{"name":"bulbasaur","img":"https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/1.png"}]
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
            console.log(url);
            
        }
    },
}
</script>

<style >
*{
    font-family: 'Turret Road', cursive;
}

.list{
    flex: 0.35;
}

.detail{
    flex: 1;
    border: 1px solid black;
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
    background: #e45a5a;
    margin:30px auto; 
    display: flex;
    box-shadow: 1px 1px 4px 1px rgba(0,0,0,0.75);
}

.pokemon{    
    width: 10vw;
    height: 15vh;
    margin: 30px 30px;
    background: rgba(206, 89, 89, 0.924);
    border: 2px solid white;
    border-radius: 10px;
    display:flex;
    flex-direction: column;
    align-items: center;
    box-shadow: 1px 1px 4px 1px rgba(0,0,0,0.75);
}




</style>