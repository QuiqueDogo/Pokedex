<template>
  <div class="container">
    <input v-model="filter">
    <div 
      class="grid"
      v-for="(post, index) in PokemonsFilter"
      :key="index">
      <card :name="post.name" :url="post.url" />
    </div>
  </div>
</template>

<script>
import Logo from '~/components/Logo.vue' 
import Card from '~/components/Card.vue'

export default {
  components: {
    Logo,
    Card
  },
  data(){
    return {
      filter:"",
      post:[],
    }
  },

created() {
  this.$axios.$get('/pokemon/?limit=10')
  .then(response => {
    this.post = response.results, 
    console.log(response)
  })
  .catch(e => console.log(e))
},
  computed:{
    PokemonsFilter(){
      if (this.post.length > 0 ) {
        if(!this.filter ){
          return this.post
        }
        return  this.post.filter(item => {
         if(item.name.indexOf(this.filter) > 0) {
            return item
          }else return ""
          }
        )
      }
      return false 
    }
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
  grid-gap: 50px;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
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
