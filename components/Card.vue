<template>
    <div class="card">
        <div class="main">
            <div class="info">
                <div class="subinfo">
                <p>{{name}}</p>
                </div>
                <div class="subinfo2">
                <h5 >Stats</h5>
                <p>{{url}}</p>
                </div>
            </div>
            <div class="image">
                <img class="pokemon" :src="img" alt="" srcset="">
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

<script>
import axios from "axios";
export default {
    data(){
        return {
            img:[]
        }
    },
    props:["name","url"],
    created(){
        axios.get(`${this.$props.url}`)
        .then(response => {this.img = response.data.sprites.front_default,console.log(response)})
        .catch(e => console.log(e))
        console.log(this.$props.url);
    }
}




</script>

<style >

p{
    font-size: 14px;
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
    flex:0.5;
    padding-top: 15px;
}

.subinfo2{
    flex:1;
    padding-top: 15px;
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