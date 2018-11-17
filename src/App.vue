<template>
  <div id="app">
    <nav>
      <router-link v-bind:to="'/'">Matt Cos</router-link>
      <router-link v-bind:to="'/projects'">Projects</router-link>
      <router-link v-bind:to="'/about'">About</router-link>
      <router-link v-bind:to="'/contact'">Contact</router-link>
      <router-link v-bind:to="'/blog'">Blog</router-link>
    </nav>
    <!-- <router-link v-bind:to="'/param'">Param</router-link> -->
    <!-- the router outlet, where all matched components would ber viewed -->
    <router-view></router-view>

    <h1>footer</h1>
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
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
