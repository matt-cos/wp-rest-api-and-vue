<template>
  <div id="projects">
    <div class="row">
      <div class="column column-75 column-offset-25">
        <h1>Projects</h1>
      </div>
    </div>

   <!--  <section v-if="errored">
      <p>We're sorry, we're not able to retrieve this information at the moment, please try back later</p>
    </section>

    <section v-else>
      <div v-if="loading">Loading...</div>

      <div v-else v-for="post in info">
        <p>{{ post.title.rendered }}</p>
        <img :src="post._embedded['wp:featuredmedia']['0'].source_url" :alt="post._embedded['wp:featuredmedia']['0'].alt_text">
      </div>

    </section> -->

     <div v-if="errored">
      <div class="row">
        <div class="column column-75 column-offset-25">
          <p>We're sorry, we're not able to retrieve this information at the moment, please try back later</p>
        </div>
      </div>
    </div>

    <div v-else class="row recent">
      <div class="column column-75 column-offset-25">
        <h2>Recent Work</h2>
        <div v-if="loading">
          <div class="row">
            <div class="column">
              <div>Loading...</div>
            </div>
          </div>
        </div>

        <div v-else v-for="post in info">
          <p>{{ post.title.rendered }}</p>
          <img :src="post._embedded['wp:featuredmedia']['0'].source_url" :alt="post._embedded['wp:featuredmedia']['0'].alt_text">
        </div>
      </div>
    </div>

    <!-- <small>{{ info }}</small> -->

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
  /*font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;*/
}
</style>
