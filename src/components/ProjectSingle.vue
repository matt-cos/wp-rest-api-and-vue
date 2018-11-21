<template>
  <div id="project-single">
    <div class="row">
      <div class="column column-75 column-offset-25">
        <h1>Project Single</h1>
      </div>
    </div>

     <div v-if="errored">
      <div class="row">
        <div class="column column-75 column-offset-25">
          <p>We're sorry, we're not able to retrieve this information at the moment, please try back later</p>
        </div>
      </div>
    </div>

    <div v-else class="row recent">
      <div class="column column-75 column-offset-25">
        <h2>{{ $route.params.id }}</h2>
        <div v-if="loading">
          <div class="row">
            <div class="column">
              <div>Loading...</div>
            </div>
          </div>
        </div>

        <div v-else>
          <h3>{{ $route.params.id }}</h3>
        </div>
      </div>
    </div>

    <!-- <small>{{ info }}</small> -->

  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'projectsingle',
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
#project-single {
  /*font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;*/
}
</style>
