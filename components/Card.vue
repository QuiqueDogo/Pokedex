<template>
    <div class="card">
        <div class="main">
            <div class="info">
                <p style="flex:0.8">Nombre Pokimon</p>
                <p style="flex:0.2">Nombre Pokimon</p>
                <p style="flex:2">Nombre Pokimon</p>
            </div>
            <div class="image">
                <img class="pokemon" src="https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/1.png" alt="" srcset="">
            </div>
        </div>
        <div class="options">
            <button class="division">
                <p>Capturar</p>
            </button>
            <button class="division2">
                <p>Atacar</p>
            </button>
        </div>
    </div>
</template>

<style >


.card{
    box-sizing: content-box;
    height: 180px;
    width: 300px;
    background-color: white;
    border:1.9px solid #bdbdbd9b;
    border-radius: 10px
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
}

.image{
    padding-top: 15px;
    width: 40%;
}

.pokemon{
    background: #bdbdbd9b;
    height: 100px;
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
    flex: 1;
    background: #f8f8f8;
    border: none;
    border-bottom-left-radius: 10px;
    border-bottom-right-radius: 10px;
    padding-right: 30%;
}
.division2{
    flex: 1;
    background: #f8f8f8;
    border: none;
    border-bottom-left-radius: 10px;
    border-bottom-right-radius: 10px;
    padding-left: 28%;
}
</style>