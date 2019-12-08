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
                <img :class="pokemon" :src="img" alt="" srcset="">
                <img :class="pokeball" src="~/static/poke.png" alt="" srcset="">
            </div>
        </div>
        <div class="options">
            <button :disabled="disableAttack" v-on:click="Capture" class="division">
                Capturar
            </button>
            <button v-on:click="Attack" class="division2">
                Atacar
            </button>
        </div>
    </div>
</template>

<script>
export default {
    data(){
        return {
            pokemon:'pokemon',
            pokeball:'pokeball',
            img:[],
            stats:[{base_stat:1}],
            hp:[{base_stat:1}],
            moves:[{move:{name:"cut"}},{move:{name:"cut"}},{move:{name:"cut"}}],
            disableAttack:false
        }
    },

    props:["name","url","index"],

    created(){
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
                this.pokemon += ' magic'
                this.NewLocalStorage(this.$props.name, this.img, this.$props.url);
                setTimeout(() => {
                    this.pokeball += " pokeballshow"
                }, 800);
            }else {
                alert("Necesitas bajarle mas vida");
            }
        },
        NewLocalStorage: function (name, image, url){
            let newPokemon;
            newPokemon = this.GetLocalPokemons();
            console.log(newPokemon.length);
            if (newPokemon.length <= 10) {
                newPokemon.push({name:name, img:image, url:url})
                localStorage.setItem("pokemonList", JSON.stringify(newPokemon))
                this.disableAttack = true;
            }else {
                alert("Ya tienes capturados 10 pokemons");
            }
            
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

// magic
// pokeballshow


</script>

<style >

@keyframes Bounces {
    0%{
        transform:scale(1);
    }
    60%{
        transform: scale(1.2);
        opacity: 1;
    }
    100%{
        transform: scale(0);
        opacity: 0;
    }
}

@keyframes BouncesPokeball {
    0%{
        transform: scale(0);
        opacity: 0;
    }
    60%{
        transform: scale(1.3);
        opacity: 1;
    }
    100%{
        transform:scale(1);
        opacity: 1;
    }
}



.magic{
    animation-duration: 0.8s;
    animation-name: Bounces;
    animation-fill-mode: forwards
}

.pokeballshow{
    animation-duration: 0.5s;
    animation-name: BouncesPokeball;
    animation-fill-mode: forwards
}

.pokeball{
    position: relative;
    top: -70px;
    width: 60px;
    height: 60px;
    opacity: 0;
}

button{
    cursor: pointer;
}

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
    box-shadow: 0 1px 8px rgba(0,0,0,0.2)
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
    padding: 8px;
    border-right: 1px solid #dbdbdb;
    text-transform: capitalize;
    
}

.image{
    padding-top: 15px;
    width: 40%;
    position: relative;
}

.pokemon{
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