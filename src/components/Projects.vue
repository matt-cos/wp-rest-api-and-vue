<template>
  <div id="projects">
    <h1>projects</h1>
    <p>When you have a great story about how your product or service was built to change lives, share it. The "About Us" page is a great place for it to live, too. Good stories humanize your brand, providing context and meaning for your product. What’s more, good stories are sticky -- which means people are more likely to connect with them and pass them on.</p>

    <section v-if="errored">
      <p>We're sorry, we're not able to retrieve this information at the moment, please try back later</p>
    </section>

    <section v-else>
      <div v-if="loading">Loading...</div>

      <div
        v-else
        v-for="post in info"
      >
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
  name: 'projects',
  data () {
    return {
      info: null,
      loading: true,
      errored: false
    }
  },
  filters: {
    currencydecimal (value) {
      return value.toFixed(2)
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
      .finally(() => this.loading = false)
  }
  // https://vuejs.org/v2/cookbook/using-axios-to-consume-apis.html
}

</script>
<!-- styling for the component -->
<style>
#projects {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
