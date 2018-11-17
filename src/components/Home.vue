<template>
  <div class="hello">
    <h1>{{ headline }}</h1>
    <p>{{ headlineCopy }}</p>

    <section v-if="errored">
      <p>We're sorry, we're not able to retrieve this information at the moment, please try back later</p>
    </section>

    <section v-else>
      <h2>Recent Work</h2>
      <div v-if="loading_section_1">Loading...</div>

      <div
        v-else
        v-for="post in info.slice(0, 6)"
      >
      <!-- slice limits it to 6 posts -->
        <p>{{ post.title.rendered }}</p>
        <img :src="post._embedded['wp:featuredmedia']['0'].source_url" :alt="post._embedded['wp:featuredmedia']['0'].alt_text">
      </div>

      <h2>Services</h2>

      <h2>Clients</h2>

      <h2>Let's Get in Touch</h2>

    </section>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'HelloWorld',
  data () {
    return {
      headline: 'Intro Text Headline',
      headlineCopy: 'Lorem ipsum dolor sit amet, consectetur adipisicing elit. Consectetur, voluptates.',
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
