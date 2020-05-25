<template>
  <div id="app">
    <header>
      <h1> Vuejs SPA</h1>
    </header>
    <main>
      <aside class="sidebar"> 
        <router-link 
        v-for="(post, index) in posts"
        v-bind:key="index"
        active-class="is-active"
        class="link"
        :to="{ name: 'post', params: { id: post.id } }">
        {{post.id}}. {{post.title}}
        </router-link>
      </aside>

      <div class="content">
        <router-view></router-view>
      </div>
    </main>
  </div>
</template>

<script>

  import axios from 'axios' 
  export default {
    data(){
      return {
        posts:null, 
        endpoint: 'https://jsonplaceholder.typicode.com/posts/'
      }
    },
    created(){
      this.getAllPosts()
    },

    methods: {
      getAllPosts(){
        axios.get(this.endpoint)
        .then(response => {
          this.posts = response.data;
        })
        .catch(error =>{
          console.log('-----error-------');
          console.log(error);
        })
      }
    }
  }
</script>

<style lang="scss" scoped>

#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
h1, h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}

</style>