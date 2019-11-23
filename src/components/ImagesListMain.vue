<template>
  <div id="app">
    <header>
      <img class="logo" src="../assets/logo.png" alt="" />ue Picsum
    </header>
    <div class="main">
      <ImageList />
    </div>
    <footer>
      Vue test project by <strong> Hasip Timurtaş </strong> for front-end
      feveloper jop position at Videoslots Ltd.
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
  text-align: center;
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}

header {
  width: 100%;
  height: 100px;
  background-color: #2c3e50;
  color: #41b883;
  text-align: center;
  font-size: 2.9rem;
}

header .logo {
  width: 100px;
}

.main {
  margin-top: 50px;
}

footer {
  width: 100%;
  height: 50px;
  background-color: #2c3e50;
  color: #ffffff;
  text-align: center;
  padding-top: 25px;
}
</style>
