<template>
  <div id="home">
    <div class="row headline">
      <div class="column column-75 column-offset-25">
        <h1>{{ headline }}</h1>
        <p>{{ headlineCopy }}</p>
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
        <h2>Recent Work</h2>
        <div v-if="loading_section_1">
          <div class="row">
            <div class="column column-33">
              <p>Loading...</p>
              <img src="" alt="Placeholder">
            </div>
            <div class="column column-33">
              <p>Loading...</p>
              <img src="" alt="Placeholder">
            </div>
            <div class="column column-33">
              <p>Loading...</p>
              <img src="" alt="Placeholder">
            </div>
          </div>
          <div class="row">
            <div class="column column-33">
              <p>Loading...</p>
              <img src="" alt="Placeholder">
            </div>
            <div class="column column-33">
              <p>Loading...</p>
              <img src="" alt="Placeholder">
            </div>
            <div class="column column-33">
              <p>Loading...</p>
              <img src="" alt="Placeholder">
            </div>
          </div>
        </div>

        <div v-else>
          <div class="row">
            <div v-for="(post, index) in info.slice(0, 3)" class="column column-33">
              <p>{{ post.title.rendered }}</p>
              <img :src="post._embedded['wp:featuredmedia']['0'].source_url" :alt="post._embedded['wp:featuredmedia']['0'].alt_text">
            </div>
          </div>
          <div class="row">
            <div v-for="(post, index) in info.slice(3, 6)" class="column column-33">
              <p>{{ post.title.rendered }}</p>
              <img :src="post._embedded['wp:featuredmedia']['0'].source_url" :alt="post._embedded['wp:featuredmedia']['0'].alt_text">
            </div>
          </div>
        </div>
      </div>
    </div>

    <div class="row services-title">
      <div class="column column-75 column-offset-25">
        <h2>Services</h2>
        <p>{{ servicesCopy }}</p>
      </div>
    </div>

    <div class="row services-content">
      <div class="column column-25 column-offset-25">WordPress</div>
      <div class="column column-25">Shopify</div>
      <div class="column column-25">Etcetera</div>
    </div>

    <div class="row clients-title">
      <div class="column column75 column-offset-25">
        <h2>Clients</h2>
      </div>
    </div>

    <div class="row clients-content">
      <div class="column column-25 column-offset-25">1</div>
      <div class="column column-25">2</div>
      <div class="column column-25">3</div>
    </div>
    <div class="row clients-content">
      <div class="column column-25 column-offset-25">4</div>
      <div class="column column-25">5</div>
      <div class="column column-25">6</div>
    </div>

    <div class="row contact-title">
      <div class="column column75 column-offset-25">
        <h2>Let's Get in Touch</h2>
      </div>
    </div>

  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'HelloWorld',
  data () {
    return {
      headline: 'Intro Text Headline',
      headlineCopy: 'Lorem ipsum dolor sit amet, consectetur adipisicing elit. Ea recusandae natus architecto iste quibusdam? Atque officia dolores repellat consequatur officiis, assumenda, odio molestiae labore ipsum consectetur provident excepturi enim delectus itaque sapiente veniam doloribus repellendus beatae, magni possimus, laboriosam. Eius quas deleniti porro, recusandae, tempora veniam eum totam hic fuga in odio. Velit praesentium laboriosam totam natus laudantium vitae, in maxime sapiente doloribus ratione dolor cum quibusdam sit rem doloremque, dignissimos! Debitis sed molestiae minima, ut, pariatur animi cum dignissimos ex nam sapiente possimus nobis eligendi, veritatis consequatur mollitia doloremque laboriosam iste culpa tempore repudiandae. Incidunt dicta ipsa veritatis corporis.',
      servicesCopy: 'Lorem ipsum dolor sit amet, consectetur adipisicing elit. Ea recusandae natus architecto iste quibusdam? Atque officia dolores repellat consequatur officiis, assumenda, odio molestiae labore ipsum consectetur provident excepturi enim delectus itaque sapiente veniam doloribus repellendus beatae, magni possimus, laboriosam. Eius quas deleniti porro, recusandae, tempora veniam eum totam hic fuga in odio. Velit praesentium laboriosam totam natus laudantium vitae, in maxime sapiente doloribus ratione dolor cum quibusdam sit rem doloremque, dignissimos! Debitis sed molestiae minima, ut, pariatur animi cum dignissimos ex nam sapiente possimus nobis eligendi, veritatis consequatur mollitia doloremque laboriosam iste culpa tempore repudiandae. Incidunt dicta ipsa veritatis corporis.',
      info: null,
      loading_section_1: true,
      errored: false
    }
  },
  mounted () {
    axios
      // .get('https://bmwmovement.org/wp-json/wp/v2/posts?_embed')
      .get('https://bmwmovement.org/wp-json/wp/v2/posts?_embed&filter[posts_per_page]=6') // limits call to 6
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
