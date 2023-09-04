<template>
  <div id="app">
    <nav-bar/>
    <main-component/>
  </div>
</template>

<script lang="ts">
import {Options, Vue} from 'vue-class-component';
import NavBar from "@/components/NavBar.vue";
import MainComponent from "@/components/MainComponent.vue";

@Options({
  components: {MainComponent, NavBar}
})
export default class App extends Vue {
}
</script>

<style lang="scss">
*{
  transition: .5s !important;
}
#app {
  overflow: auto;
  height: 100vh;
}
body {
  height: 100vh;
  margin: 0;
  background-color: #F8F8FF;
  overflow: hidden;
}
</style>
