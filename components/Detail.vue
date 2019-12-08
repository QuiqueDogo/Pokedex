<template>
    <div class="container">
        <div class="backimg">
            <p class="text">Pokemon Capturado</p>
        </div>
        <div class="subcontainer">
            <div class="img">
                <img class="imgpokemon" :src="(sprites != '') ? sprites: require('~/static/poke.png') " alt=" ">
            </div>
            <div class="info">
                <div class="name">
                    <img class="pokeball" src="~/static/poke.png" alt="">
                    <p class="pokemonName">No. {{info.id}} {{info.name}}</p>
                    <p class="weight">Peso {{info.weight}} kg</p>
                </div>
            </div>
        </div>
        <div class="info">
            <div class="imgbacks">
                <p>All Sprites</p>
                <img
                class="all"
                v-for="(element, index) in allsprites"
                :key="index"
                :src="element"
                alt=" "
                >
            </div>
        </div>
    </div>
</template>

<script>
export default {
    props:['info','sprites','allsprites']
}
</script>

<style scoped>
.container{
    width: 80%;
    height: 80%;
    border: 2.6px solid black;
    border-radius: 15px;
    margin:  50px auto;    
    background-image: url("~@/static/cuadricula.jpg");
    box-shadow: 10px 10px 9px 0px rgba(0,0,0,0.24);
}

.backimg{
     width: 100%;
     height: 40px;
     background: linear-gradient(to bottom , #4c59f4 40%, #3543c4 45%,#3543c4 60%,#272e94 70%);
     border-top-left-radius: 15px;
     border-top-right-radius: 15px;
     border: 2.6px solid #272e94;
}
.text{
    color: white;
    font-size: 20px;
    letter-spacing: 1.2px;
    font-weight: 600;
    padding: 5px 30px;
}
.subcontainer{
    width: 100%;
    height: 40%;
    display: flex;
    flex-direction: row1;
}
.img{
    flex: 0.6;
    display: flex;
    align-items: center;
    justify-content: center;
}
.imgpokemon{
    height: 230px;
    width: 230px;
}
.info{
    flex: 1;
    display: flex;
    justify-content: center;
    align-items: center;
    padding: 10px;
}
.name{
    width: 88%;
    height: 75px;
    border: 3px solid #000;
    border-radius: 10px;
    display: flex;
    background: linear-gradient(to bottom , #e53133 50%,#f6969e 54%,#f6969e 58%,white 60%)
}
.pokeball{
    width: 20px;
    height: 20px;
    margin: 10px;
}
.pokemonName{
    margin: 7px;
    color: white;
    text-transform: capitalize;
    font-size: 20px;
    font-weight: 600;
    letter-spacing: 1.2px;
    text-shadow: 0px 3px 0px rgba(150, 150, 150, 1);
}
.weight{
    width: auto;
    margin-top: 43px;
    bottom: 0;
    left: 0;
    color: rgb(0, 0, 0);
    font-size: 20px;
    font-weight: 600;
    letter-spacing: 1.2px;
    text-shadow: 0px 3px 0px rgb(192, 192, 192);

}
.imgbacks{
    width: 88%;
    height: 230px;
    padding-left: 50px;
    padding-top: 40px;
    border: 4px solid #000;
    border-radius: 10px;
    background: linear-gradient(to right , #e53133 2.5%,#f6969e 3.5%,#f6969e 3.5%,white 5%,white 95%,#f6969e 96.5%, #f6969e 96.5%,#e53133 98.5%)
}
.all{
    height: 80px;
    width: 80px;
}
</style>