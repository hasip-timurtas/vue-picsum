<template>
  <div>
    <input class="filterbar" type="text" v-model="filterText" placeholder="Filter by Author" />
    <Navigation
      :currentPage="currentPage"
      :lastPage="lastPage"
      :perPage="perPage"
      @update-current-page="updatePage"
      @update-per-page="onPerPageChange"
    />
    <div class="row">
      <image-item
        v-for="picsumImage in filteredImages"
        :key="picsumImage.id"
        :picsumImage="picsumImage"
        @show-modal="showModal"
      />
    </div>
    <Navigation
      :currentPage="currentPage"
      :lastPage="lastPage"
      :perPage="perPage"
      @update-current-page="updatePage"
      @update-per-page="onPerPageChange"
    />
    <modal name="picsum-modal" width="80%" height="80%">
      <iframe :src="selectedImageUrl" width="100%" height="100%" />
    </modal>
  </div>
</template>
<script>
import axios from "axios";
import Navigation from "./Navigation.vue";
import ImageItem from "./ImageItem";
export default {
  name: "ImageList",
  components: {
    Navigation,
    "image-item": ImageItem
  },
  data() {
    return {
      images: [""],
      selectedImageUrl: "",
      currentPage: 1,
      perPage: "30",
      lastPage: false,
      filterText: ""
    };
  },
  methods: {
    getImages() {
      const url = `https://picsum.photos/v2/list?page=${this.currentPage}&limit=${this.perPage}`;
      axios
        .get(url)
        .then(res => {
          this.lastPage = res.data.length < this.perPage;
          this.images = res.data;
        })
        .catch(e => {
          // eslint-disable-next-line no-console
          console.log(e);
        });
    },
    showModal(url) {
      this.selectedImageUrl = url;
      this.$modal.show("picsum-modal");
    },
    onPerPageChange(event) {
      this.perPage = event.target.value;
    },
    updatePage(page) {
      this.currentPage = page;
    }
  },
  watch: {
    currentPage: {
      immediate: true,
      handler() {
        this.getImages();
      }
    },
    perPage() {
      this.getImages();
    }
  },
  computed: {
    filteredImages() {
      return this.images.filter(
        image =>
          image.author &&
          image.author.toLowerCase().includes(this.filterText.toLowerCase())
      );
    }
  }
};
</script>

<style lang="scss" scoped>
.filterbar {
  width: 40%;
  height: 50px;
  font-size: 1.5rem;
  border: 2px solid #bde8d5;
  border-radius: 25px;
  padding-left: 15px;
  color: grey;
}
.row {
  display: flex;
  flex-wrap: wrap;
}
</style>
