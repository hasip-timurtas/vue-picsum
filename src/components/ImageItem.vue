<template>
  <div class="col">
    <img
      :url="picsumImage.url"
      :src="'https://picsum.photos/id/' + picsumImage.id + '/367/267'"
      alt
      @click="onImageClick"
    />
    <div class="container">
      <h4>
        <b>{{ picsumImage.author }}</b>
      </h4>
      <p>#{{ picsumImage.id }}</p>
    </div>
  </div>
</template>

<script>
export default {
  name: "SingleImage",
  props: {
    picsumImage: {
      type: Object,
      required: true
    }
  },
  methods: {
    onImageClick(event) {
      const imgElement = event.currentTarget;
      const picsumUrl = imgElement.getAttribute("url");
      const byPassFrameUrl = "https://jsonp.afeld.me/?url=";
      const url = byPassFrameUrl + picsumUrl;
      this.$emit("showModal", url);
    }
  }
};
</script>

<style lang="scss" scoped>
.col {
  flex: 1 0 10%;
  margin: 5px;
  align-items: center;
  justify-content: center;
}
.col img {
  width: 367px;
  height: 267px;
  cursor: pointer;
}
</style>
