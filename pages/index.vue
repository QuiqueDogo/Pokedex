<template>
  <div class="contain" >
    <div class="search">
      <img src="~/static/icon.png" class="icon" />
      <input class="modesearch" v-model="filter" type="text" @keydown="search()"> 
    </div>
  <div class="container">
    <div 
      class="grid"
      v-for="(post, index) in filterPost"
      :key="index">
      <card :name="post.name" :url="post.url" :key="post.name" />
    </div>
  </div>
  <audio loop autoplay :src="require('~/static/Route.mp3')" />
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
      filterPost:[]
    }
  },

  created() {
    this.$axios.$get('/pokemon/?limit=49')
    .then(response => {
      this.post = response.results
      this.filterPost = response.results;
    })
    .catch(e => console.log(e))

  },

  methods:{
    search(){
      this.filterPost = [];
  
      this.post.map(item => {
        if (this.filter == '' || this.filter == ' ') {
          this.filterPost = this.post
				} else {
          if (item.name.toUpperCase().indexOf(this.filter.toUpperCase()) > -1) {
            this.filterPost.push(item)
					}
        }
      })
    },
  },

  mounted() {
    this.post.map( item => {
      this.filterPost.push(item)
    })
  }
}
</script>

<style>
*{
  font-family: 'Open Sans', cursive;
}
.search{
  display: flex;
  justify-content: flex-end;
  justify-items: center;
  margin: 20px 30px;
}

.icon{
  height: 25px;
  width: 25px;
  position: relative;
  left: 15%;
  top: -2px;
}

.modesearch{
  border: 0;
  border-bottom: 1px solid #bdbdbd;
  padding-left: 10px;
  padding-bottom: 3px;
  transition: 0.5s ease-in;
}

.modesearch:focus{
  border-color: #FF6363;
}

.container {
  box-sizing: border-box;
  margin: 0 50px;
  max-height: 100%;
  max-width: 100vw;
  display: grid;
  grid-gap: 20px;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  text-align: center;
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
