<template lang="pug">
  .hello
    img(src="../assets/logo.jpg" width="300px" height="300px")
    h1 {{ msg }}
    h2 Essential Links
    ul
      li
        a(href="https://twitter.com" target="_blank") Twitter
      li
        a(href="https://facebook.com" target="_blank") Facebook
    h2 Recent Articles
    ul
      li(v-for="item in items")
        a(:href="postPath(item)") {{item.title}}
</template>

<script>
import Vue from 'vue'
import axios from 'axios'
import VueAxios from 'vue-axios'

Vue.use(VueAxios, axios)

const BLOG_ID = '819751833423889054';
const API_KEY = 'AIzaSyDSEiq6j_xAyNAAcz_1cyRzfIecHotCB6o';
var api = "https://www.googleapis.com/blogger/v3/blogs/"+BLOG_ID+"/posts";

export default {
  name: 'HelloWorld',
  data(){
    return {
      msg: 'Omnivorous Tech',
      body: 'Comming Soon...',
      items: []
    }
  },
  methods: {
    postPath(item){
      return "/#/post/" + item.id
    }
  },
  mounted(){
    Vue.axios.get(api,{params:{key: API_KEY}}).then((response) => {
      this.items = response.data.items
    })
  }
}


</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
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
