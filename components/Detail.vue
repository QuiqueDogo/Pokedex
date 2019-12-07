<template>
    <div class="container">
        <div class="backimg">
            <p class="text">Pokemon Capturado</p>
        </div>
        <div class="subcontainer">
            <div class="img">
                <img class="imgpokemon" src="https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/2.png" alt="">
            </div>
            <div class="info">
                <div class="name">
                    <img class="pokeball" src="~/static/poke.png" alt="">
                    <p>Puto</p>
                </div>
            </div>
        </div>
    </div>
</template>

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
    padding: 10px 30px;
}
.subcontainer{
    width: 100%;
    height: 55%;
    border: 1px solid red;
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
    padding: 10px;
    border:1px solid purple;
}
.name{
    width: 80%;
    height: 70px;
    border: 3px solid #000;
    border-radius: 10px;
    display: flex;
    background: linear-gradient(to bottom , #e53133 50%,#f6969e 54%,#f6969e 58%,white 60%)
}
.pokeball{
    width: 20px;
    height: 20px;
}

</style>