<template>

  <nav>
    <div class="menu-list">
      <div class="menu-item">ACME Corp</div>
    </div>
  </nav>

</template>

<script>

import {Options, Vue} from "vue-class-component";

@Options({})

export default class NavBar extends Vue {

}

</script>

<style scoped lang="scss">

nav {
  background-color: gray;
  height: 96px;

  .menu-list {
    display: flex;
    flex-direction: row;
    height: 100%;
  }

  .menu-item {
    margin: auto 32px;
    height: 32px;
    text-align: center;
  }

}

</style>