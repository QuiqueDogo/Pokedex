<template>
    <div class="header">
        <div class="containerLogo">
            <img class="logo" src="http://pixelartmaker.com/art/d98dde45d242734.png">
        </div>
        <div class="choose">
            <p>Batalla y captura tu pokemon</p>
        </div>
        <div class="menu">
            <a style="width:auto;"  :class="activeBar" href="/">Pokemons</a>
            <a style="width:auto;" :class="activeBar2" href="/ListPokemon">Mis Pokemons</a>
        </div>
    </div>
</template>

<script>

export default {
    data(){
        return{
            activeBar: '',
            activeBar2: '',
            }
    },
    created() {
        
        if(this.$root._route.name == "index"){
            this.activeBar = 'active'
        }else if(this.$root._route.name == "ListPokemon"){
            this.activeBar2 = 'active'
        }
  },
}
</script>

<style scoped>
.active{
    box-shadow: 0 3px 0 rgba(54, 52, 52, 0.828);
    transition: 0.2s ease-in;
}

a{  
    text-align: center;
    color:rgba(224, 218, 218, 0.87);
    margin: 0 20px;
    text-decoration: none;
    text-transform: capitalize;
    transition: 0.2s ease-in;
    padding: 7px 0 0 0;
    height: 30px;
}

a:visited{
    color:rgb(235, 228, 228);
}

a:hover{
    box-shadow: 0 3px 0 rgba(54, 52, 52, 0.828);
    cursor: pointer;
}

.Pok{
    color: white;
}

p{
    font-size: 14px;
}

.header{
    padding:10px;
    display: flex;
    width:100%;
    height:50px;
    background: #FF6363;
    position: sticky;
    top: 0;
    z-index: 5;
}

.logo{
    min-width: 120px;
    max-height: 50px;
    object-fit: contain;
}

.containerLogo{
    flex:1;
    display: flex;
    justify-content: flex-start;
    margin-left: 30px;
}

.choose{
    flex:1;
    padding:5px 0;
    letter-spacing: 1px; 
    text-align: center;
    font-weight: bolder;
    color: white;
}

.menu{
    flex:1;
    padding-right: 37px;
    display: flex;
    justify-content: flex-end;
    font-weight: bolder;
}

</style>