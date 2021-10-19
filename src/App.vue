<template>
  <NavBar/>
  <ParticipantList/>
</template>

<script lang="ts">
import {Options, Vue} from 'vue-class-component';
import NavBar from "./components/NavBar.vue";
import ParticipantList from "./components/ParticipantList.vue"

@Options({
  components: {
    NavBar,
    ParticipantList
  },
})
export default class App extends Vue {
}
</script>

<style lang="scss">
html, body {
  margin: 0;
  padding: 0;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;

  background-color: #f2f2f2;
  height: 100%;

}

button {
  height: 40px;
  margin: 16px 16px 16px auto;
  border: none;
  text-align: center;
  padding: 8px;
  font-weight: bold;

  &:hover {
    background-color: gray;
  }
}


</style>
