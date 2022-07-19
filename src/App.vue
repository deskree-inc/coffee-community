<template>
  <router-view/>
</template>

<style lang="scss">
#app {
  font-family: Karla, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;

  h1 {
    margin-top: 10px;
    margin-bottom: 15px;
    font-size: 36px;
    line-height: 50px;
    font-weight: 400;
  }
}

nav {
  padding: 30px;

  a {
    font-weight: bold;
    color: #2c3e50;

    &.router-link-exact-active {
      color: #42b983;
    }
  }
}
</style>
