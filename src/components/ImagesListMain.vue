<template>
  <div id="app">
    <div class="row">
      <input v-model.number="num1" type="number" />
      <span>+</span>
      <input v-model.number="num2" type="number" />
      <span>=</span>
      <span>{{num1 + num2}}</span>
    </div>
    <div class="row second">
      <select v-model="name">
        <option>Carne Asada</option>
        <option>Pollo</option>
        <option>Bean</option>
        <option>Al Pastor</option>
      </select>
      <p v-if="name">My Favorite kind of taco is {{name}}</p>
    </div>
  </div>
</template>

<script>
export default {
  el: "#app",
  name: "ImagesListMain",
  props: {
    msg: String
  },
  data() {
    return {
      num1: 0,
      num2: 0,
      name: ""
    };
  }
};
</script>