<template>
    <div :style="cssProps" class="card">
        <div class="main">
            <div class="info">
                <div class="subinfo">
                <p>{{name}}</p>
                <div class="containerHp">
                    <div class="HP"></div>
                </div>
                </div>
                <div class="subinfo2">
                <h5 >Stats</h5>
                <p>PH: {{hp[0].base_stat}}/{{stats[0].base_stat}}</p>
                <p>Moves: {{moves[0].move.name}}, {{moves[1].move.name}}, {{moves[2].move.name}} </p>
                </div>
            </div>
            <div class="image">
                <img class="pokemon" :src="img" alt="" srcset="">
            </div>
        </div>
        <div class="options">
            <button v-on:click="Capture" class="division">
                <p>Capturar</p>
            </button>
            <button v-on:click="Attack" class="division2">
                <p>Atacar</p>
            </button>
        </div>
    </div>
</template>

<script>
export default {
    data(){
        return {
            disable:false,
            img:[],
            stats:[{base_stat:1}],
            hp:[{base_stat:1}],
            moves:[{move:{name:"cut"}},{move:{name:"cut"}},{move:{name:"cut"}}]
        }
    },

    props:["name","url","index"],

    created(){
        console.log(localStorage.length)
        this.$axios.get(`${this.$props.url}`)
        .then(response => {
            this.img = response.data.sprites.front_default,
            this.stats = [response.data.stats[0]],
            this.hp = [response.data.stats[0]],
            this.moves = [response.data.moves[0],response.data.moves[1],response.data.moves[2]]
            })
        .catch(e => console.log(e))
    },
    computed:{
        cssProps() {
            return {
            '--life': ((this.hp[0].base_stat * 100)/this.stats[0].base_stat) + "%",
            '--color': 
            (((this.hp[0].base_stat * 100)/this.stats[0].base_stat) <= 100 && 
            ((this.hp[0].base_stat * 100)/this.stats[0].base_stat) >= 60) ? "#15e765" : 
            (((this.hp[0].base_stat * 100)/this.stats[0].base_stat) <= 59 && ((this.hp[0].base_stat * 100)/this.stats[0].base_stat) >= 30) ? "#f7de76" : "#f45639"
        }
        }
    },
    methods:{
        Attack: function (event) {
            if( this.hp[0].base_stat >= 10 ){
                this.hp = [{base_stat:(this.hp[0].base_stat -  Math.round(Math.random() * (9 - 1) + 1))}];
            }else if (this.hp[0].base_stat <= 9){
                alert(`Detente, Vas a matar a ${this.$props.name}. :(`);
            }
        },
        Capture: function (event) {
            if(((this.hp[0].base_stat * 100)/this.stats[0].base_stat) <= 45){
                console.log("Puedes atraparlo");
                this.NewLocalStorage(this.$props.name, this.img);
            }else {
                alert("Necesitas bajarle mas vida");
            }
        },
        NewLocalStorage: function (name, image){
            let newPokemon;
            newPokemon = this.GetLocalPokemons();
            newPokemon.push({name:name, img:image})
            localStorage.setItem("pokemonList", JSON.stringify(newPokemon))
            // localStorage.setItem("pokemonList", JSON.stringify([{name:name, img:image}]));
        },

        GetLocalPokemons: function (){
            let pokemons;
            if (localStorage.getItem("pokemonList") === null ) {
                pokemons = [];
            }else{
                pokemons = JSON.parse(localStorage.getItem("pokemonList"));
            }
            return pokemons;
        }

    }
}




</script>

<style >

p{
    font-size: 14px;
}

.containerHp{
    width: 90%;
    height: 11px;
    margin: 5px auto;
    position: relative;
    border-radius: 5px;
    border: 1px solid #dbdbdb;
    background: #475355;;
}

.HP{
    width: var(--life);
    height: 9px;
    position: relative;
    border-radius: 5px;
    background: var(--color);
    border: 1px solid var(--color);
    transition: 0.4s ease;
}

.card{
    box-sizing: content-box;
    height: 180px;
    width: 300px;
    background-color: white;
    border:1.9px solid #bdbdbd9b;
    border-radius: 10px;
    margin:20px;
    grid-row: 1;
}
.main{
    width: 100%;
    height: 80%;
    box-sizing: border-box;
    display: flex;
    flex-direction: row;
}

.info{
    width: 60%;
    display: flex;
    flex-direction: column;
    justify-content: flex-start;
}

.subinfo{
    flex:0.3;
    padding-top: 15px;
    text-transform: capitalize;
    border-right: 1px solid #dbdbdb;
    border-bottom: 1px solid #dbdbdb;
}

.subinfo2{
    flex:1;
    padding-top: 5px;
    border-right: 1px solid #dbdbdb;
    text-transform: capitalize;
    
}

.image{
    padding-top: 15px;
    width: 40%;
}

.pokemon{
    background: #bdbdbd9b;
    height: 100px;
    object-fit: contain;
}

.options{
    width: 100%;
    height: 20%;
    display: flex;
    flex-direction: row;
    justify-content: space-around;
    background: #f8f8f8;
    border-bottom-left-radius: 10px;
    border-bottom-right-radius: 10px;
}
.division{
    flex: 0.7;
    background: #f8f8f8;
    border: none;
    border-bottom-left-radius: 10px;
    padding-right: 30%;
    background: rgba(238, 75, 75, 0.89);
    color:white;
}
.division2{
    flex: 0.7;
    background: #f8f8f8;
    border: none;
    background: rgba(36, 35, 35, 0.835);
    color: white;
    border-bottom-right-radius: 10px;
    padding-left: 28%;
}
</style>