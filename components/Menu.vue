<template>
    <div class="header">
        <div class="containerLogo">
            <img class="logo" src="http://pixelartmaker.com/art/d98dde45d242734.png">
        </div>
        <div class="choose">
            <p>Batalla y captura tu pokemon</p>
        </div>
        <div class="menu">
            <p>hola</p>
            <a href="http://">hola</a>
        </div>
    </div>
</template>

<script>
import Hamburger from "~/components/Hamburger.vue"

export default {
    components:{
        Hamburger
    }
}
</script>

<style scoped>
.header{
    padding:10px;
    display: flex;
    width:100%;
    height:7vh;
    background-image: linear-gradient(to right, #d16b6b, #d16f6a, #d1746a, #d1786a, #d17c6a, #d17e6a, #d17f6b, #d1816b, #d1816b, #d1816b, #d1816b, #d1816b);
}

.logo{
    min-width: 120px;
    max-height: 50px;
    object-fit: contain;
}

.containerLogo{
    flex:1;
    display: flex;
    justify-content: center;
}

.choose{
    flex:1;
    padding:15px 0;
    letter-spacing: 1px; 
    text-align: center;
}

.menu{
    flex:1;
    padding:15px 0;
    padding-right: 30px;
    display: flex;
    justify-content: center;
}

</style>