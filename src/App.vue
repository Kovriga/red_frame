<template>
  <div id="app">
    <nav-bar/>
  </div>
</template>

<script lang="ts">
import {Options, Vue} from 'vue-class-component';
import NavBar from "@/components/NavBar.vue";

@Options({
  components: {NavBar}
})
export default class App extends Vue {
}
</script>

<style lang="scss">
body {
  background-color: #F8F8FF;
  overflow: hidden;
}
</style>
