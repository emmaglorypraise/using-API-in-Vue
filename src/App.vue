<template>
  <div id="app">
    <h1>Testing API in Vue</h1>

    <!-- Posting data from API in VUE -->
   <form action="" v-on:submit.prevent="submit()">
        <input type="text" v-model="form.songId" placeholder="song id"/>
        <input type="text" v-model="form.singerId" placeholder="singer id"/>
        <input type="text" v-model="form.userId" placeholder="user id"/>
        <input type="text" v-model="form.songUrl" placeholder="song url"/>
        <input type="text" v-model="form.songPic" placeholder="song pic"/>
        <input type="text" v-model="form.introduction" placeholder="introduction"/>
        <button >Submit</button>
</form>
       

<br><br>

    <input type="text" v-model="postBody" >
    <button v-on:click = "postPost()">Post</button>

<!-- Fetching data from API in VUE -->
    <ol v-if="post && post.length">
      <li v-for="post of post" :key="post.id">
        <p><strong>{{post.title}}</strong></p>
        <p>{{post.body}}</p>
      </li>
    </ol>
    <!-- <p> {{post}} </p> -->
  </div>
</template>

<script>

// import axios from '.axios';
const axios = require('axios')

export default {
  
  name: 'App',
  data () {
    return {
      post: [],
      postBody: '',
      form: {
        songId: '',
        userId: '',
        singerId: '',
        songUrl: '',
        songPic: '',
        introduction: ''
      }
    }
  },
  mounted () {
    axios.get('http://jsonplaceholder.typicode.com/posts')
      .then(response => (this.post = response.data)) 
  },
  methods: {
    
     postPost() {
      axios.post(`http://jsonplaceholder.typicode.com/posts`, {
        body: this.postBody
      })
      .then(response => console.log(response))
    },
    submit() {
      console.log(this.form)
       axios.post(`cart/add`, {
        body: this.form
      })
      .then(response => console.log(response))
    }
  }
  
}
</script>

<style>

</style>
