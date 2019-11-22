<template>
  <div id="app">
    <header>
      Vue Picsum
    </header>
    <div class="main">
      <ImageList />
    </div>
    <footer>
      <h5>
        Vue test project for front-end feveloper jop position at Videoslots Ltd.
      </h5>
    </footer>
  </div>
</template>

<script>
import ImageList from "./ImageList.vue";

export default {
  name: "ImagesListMain",
  components: {
    ImageList
  }
};
</script>

<style>
html,
body {
  padding: 0;
  margin: 0;
}
li {
  list-style-type: none;
  float: left;
}
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}

header {
  width: 100%;
  height: 50px;
  background-color: #2c3e50;
  color: white;
  text-align: center;
  font-size: 30px;
}

footer {
  width: 100%;
  height: 50px;
  background-color: #2c3e50;
  color: white;

  text-align: center;
}
</style>
