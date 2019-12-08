<template>
    <div class="container" >
        <img class="individual" src="~/static/individual.png" alt="">
        <img class="poki" :src="img" alt="">
        <div class="containerHp">
                    <div class="HP"></div>
        </div>
        <p class="name">{{this.$props.name}}</p>
    </div>
</template>

<script>
export default {
    props:["name","img"],
    
}
</script>

<style scoped>
    .container{
        width: 90%;
        height: 55px;
        margin: 30px auto;
        border: 1px solid #3f3f3f;
        border-radius: 30px;
        cursor: pointer;
        box-shadow: 1px 1px 2px 1px rgba(0,0,0,0.75);
        background: linear-gradient(to bottom, #3F92DD 60%, #7EC4DD 2%,#3F92DD 70%,#7EC4DD 10%);
    }

    .individual{
        height: 65px;
        width: 65px;
        position: absolute;
        left: 6%;
        transform: translateY(-5px);
    }
    .poki{
        z-index: 1;
        width: 120px;
        height: 120px;
        position: absolute;
        left: 4.5%;
        transform: translateY(-40px);
        
    }
    .containerHp{
        width: 29%;
        height: 14px;
        position: relative;
        border-radius: 5px;
        left: 35%;
        top: 35px;
        border: 1px solid #dbdbdb;
        background: #475355;;
    }

    .containerHp::after{
        content: "HP";
        font-weight: bolder;
        color: rgb(231, 229, 83);
        position: absolute;
        left: -25%;
        top: -8%;
        font-size: 13px;
        height: 14px;
        width: 25px;
        text-align: center;
        border-bottom-left-radius: 5px;
        border-top-left-radius: 5px;
        background: rgb(109, 108, 108);

    }

    .HP{
        width: 100%;
        height: 12px;
        position: relative;
        border-radius: 5px;
        background: #15e765;
        border: 1px solid #15e765;
        transition: 0.4s ease;
    }
    

    .name{
        position: relative;
        top: -14%;
        left: 28%;
        text-transform: uppercase;
        letter-spacing: 1.2px;
    }
</style>