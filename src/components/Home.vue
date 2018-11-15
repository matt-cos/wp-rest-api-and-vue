<template>
  <div class="hello">
    <h1>{{ msg }}</h1>

    <section v-if="errored">
      <p>We're sorry, we're not able to retrieve this information at the moment, please try back later</p>
    </section>

    <section v-else>
      <div v-if="loading_section_1">Loading...</div>

      <div
        v-else
        v-for="post in info.slice(0, 6)"
      >
      <!-- slice limits it to 6 posts -->

        {{ post.id }}

        <!-- {{ post._embedded['wp:featuredmedia']['0'].source_url }} -->
        <img :src="post._embedded['wp:featuredmedia']['0'].source_url" :alt="post._embedded['wp:featuredmedia']['0'].alt_text">
      </div>

    </section>

    <small>{{ info }}</small>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'HelloWorld',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App',
      info: null,
      loading_section_1: true,
      errored: false
    }
  },
  mounted () {
    axios
      .get('https://bmwmovement.org/wp-json/wp/v2/posts?_embed')
      .then(response => {
        this.info = response.data
      })
      .catch(error => {
        console.log(error)
        this.errored = true
      })
      .finally(() => this.loading_section_1 = false)
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
