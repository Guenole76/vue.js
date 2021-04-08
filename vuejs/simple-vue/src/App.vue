<template>
  <div>
    <div v-if="posts.length">
    <ul>
        <li
          v-for="post in posts"
          :key="post.id"
        >
          <h1 v-html="post.title.rendered"></h1>
          <p v-html="post.excerpt.rendered"></p>
        </li>
    </ul>
    </div>
    <div v-else>
      Chargement des posts…
    </div>
  </div>
</template>

<script>

export default {

  name: 'SimpleVue',
  data() {
    return {
      posts: []
    }
  },
  mounted()  {
fetch('https://relikto.com/wp-json/wp/v2/posts?' + new URLSearchParams({
  context: 'view',
  per_page: 8,
}))
  .then(response => {
    return response.json()
  })
  .then(json => {
    this.posts = json
  })
  .catch(error => console.error(error))
}

}
</script>



<style>
  h1{
    font: italic 2.2em "Fira Sans", serif;
    font-weight: bold;
    text-decoration: underline;
  }
  p{
    
    font: italic 1em "Fira Sans", serif;
  }
  #app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
  }
</style>