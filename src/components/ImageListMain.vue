<template>
  <div id="app">
    <header>
      <img class="logo" src="../assets/logo.png" alt="Vue Picsum logo" />ue Picsum
    </header>
    <main>
      <image-list />
    </main>
    <footer>
      <strong>MHT</strong>
    </footer>
  </div>
</template>

<script>
import ImageList from "./ImageList.vue";

export default {
  name: "ImagesListMain",
  components: {
    "image-list": ImageList
  }
};
</script>

<style lang="scss">
$mainColor: #2c3e50;

html,
body {
  padding: 0;
  margin: 0;
}

#app {
  text-align: center;
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: $mainColor;
}
header {
  width: 100%;
  height: 100px;
  background-color: $mainColor;
  color: #41b883;
  text-align: center;
  font-size: 2.9rem;
}
header .logo {
  width: 100px;
}
main {
  width: 95%;
  margin: 50px auto 0 auto;
}
footer {
  width: 100%;
  height: 50px;
  background-color: $mainColor;
  color: #ffffff;
  text-align: center;
  padding-top: 25px;
}

li {
  list-style-type: none;
  float: left;
}
::placeholder {
  color: #b7dacb;
}
</style>
