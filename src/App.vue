<template>
  <div id="app">
    <nav class="row">
      <div class="column column-50">
        <router-link v-bind:to="'/'">Matt Cos</router-link>
      </div>
      <div class="column">
        <router-link v-bind:to="'/projects'">Projects</router-link>
      </div>
      <div class="column">
        <router-link v-bind:to="'/about'">About</router-link>
      </div>
      <div class="column">
        <router-link v-bind:to="'/contact'">Contact</router-link>
      </div>
      <div class="column">
        <router-link v-bind:to="'/blog'">Blog</router-link>
      </div>
    </nav>
    <!-- <router-link v-bind:to="'/param'">Param</router-link> -->
    <!-- the router outlet, where all matched components would ber viewed -->
    <router-view></router-view>

    <div class="row">
      <div class="column">
        <p>Copyright Matt Cos 2018</p>
      </div>
      <div class="column">
        <a href="#!" class="float-right">LinkedIn</a>
        <a href="#!" class="float-right">GitHub</a>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'app'
}
</script>
<!-- styling for the component -->
<style>
#app {
  /*font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;*/
}
</style>
