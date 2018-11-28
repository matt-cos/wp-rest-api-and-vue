<template>
  <div id="project-single">

     <div v-if="errored">
      <div class="row">
        <div class="column column-75 column-offset-25">
          <p>We're sorry, we're not able to retrieve this information at the moment, please try back later</p>
        </div>
      </div>
    </div>

    <div v-else class="row recent">
      <div class="column column-75 column-offset-25">
        <div v-if="loading">
          <div class="row">
            <div class="column">
              <div>Loading...</div>
            </div>
          </div>
        </div>

        <div v-else>
          <h1>{{ info[0].title.rendered }}</h1>
          <!-- <img :src="info[0]._embedded['wp:featuredmedia']['0'].source_url" :alt="post._embedded['wp:featuredmedia']['0'].alt_text"> -->
          <!-- alt text was causing issues -->
          <img :src="info[0]._embedded['wp:featuredmedia']['0'].source_url">
          <div v-html="info[0].content.rendered"></div>
        </div>
      </div>
    </div>

    <!-- <a :href="pthhh"><small>{{ pthhh }}</small></a>
    <br>
    <br>
    <small>{{ info }}</small> -->

  </div>
</template>

<script>
import axios from 'axios'

// var pathName = window.location.pathname.replace('/projects/','https://bmwmovement.org/wp-json/wp/v2/posts?slug=');
var pathName = window.location.pathname.replace('/projects/','https://bmwmovement.org/wp-json/wp/v2/posts?_embed&slug=');

export default {
  name: 'projectsingle',
  data () {
    return {
      info: null,
      loading: true,
      errored: false,
      pthhh: pathName
    }
  },
  filters: {
    currencydecimal (value) {
      return value.toFixed(2)
    }
  },
  mounted () {
    axios
      .get(pathName)
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
#project-single {
  /*font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;*/
}
</style>
