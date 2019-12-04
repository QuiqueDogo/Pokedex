<template>
  <div class="container">
    <div 
      class="grid"
      v-for="(post, index) in post"
      :key="index">
      <card :name="post.name" :url="post.url" />
    </div>
  </div>
</template>

<script>
import axios from "axios";
import Logo from '~/components/Logo.vue' 
import Card from '~/components/Card.vue'

export default {
  components: {
    Logo,
    Card
  },
  data(){
    return {
      post:[],
    }
  },

created() {
  axios.get('https://pokeapi.co/api/v2/pokemon/?limit=51')
  .then(response => {this.post = response.data.results})
  .catch(e => console.log(e))
}

}
</script>

<style>
.container {
  box-sizing: border-box;
  margin: 0 auto;
  max-height: 100%;
  max-width: 100vw;
  display: grid;
  grid-template-columns: auto auto auto;
  text-align: center;
  border: 1px solid #dbdbdd;
}

.grid{
  margin: 0 auto;
}

.title {
  font-family: 'Quicksand', 'Source Sans Pro', -apple-system, BlinkMacSystemFont,
    'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif;
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}
</style>
