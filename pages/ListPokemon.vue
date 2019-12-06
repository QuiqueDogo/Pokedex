<template>
    <div class="container-pok">
        <div 
        class="pokemon"
        v-for="(element, index) in pokemonSave"
        :key="index"
        >
            <div class="image">
                <img :src="element.img">
            </div>
            <div class="text">
                <p>{{element.name}}</p>
            </div>
        </div>
    </div>
</template>

<script>
export default {
  
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
                console.log(this.pokemonSave);
            }
      }
  },
}
</script>

<style scoped>


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
    height: 100%;
    width: 90%;
    background: #883a3a;
    margin:30px auto; 
    display: grid;
    grid-gap: 50px;
    border-radius: 10px;
    grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
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