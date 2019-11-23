<template>
  <div>
    <input class="filterbar" type="text" v-model="filterText" placeholder="Filter by Author" />
    <Nav
      :page="page"
      :lastPage="lastPage"
      :perPage="perPage"
      @updatePage="updatePage"
      @onPerPageChange="onPerPageChange"
    />
    <div class="row">
      <SingleImage v-for="p in filteredImages" :key="p.id" :p="p" @showModal="showModal" />
    </div>
    <Nav
      :page="page"
      :lastPage="lastPage"
      :perPage="perPage"
      @updatePage="updatePage"
      @onPerPageChange="onPerPageChange"
    />
    <modal name="picsum-modal" width="80%" height="80%">
      <iframe :src="selectedImageUrl" width="100%" height="100%" />
    </modal>
  </div>
</template>
<script>
import axios from "axios";
import Nav from "./Nav.vue";
import SingleImage from "./SingleImage";
export default {
  name: "ImageList",
  components: {
    Nav,
    SingleImage
  },
  data() {
    return {
      images: [""],
      selectedImageUrl: "",
      page: 1,
      perPage: 30,
      lastPage: false,
      filterText: ""
    };
  },
  created() {
    this.getImages();
  },
  methods: {
    getImages() {
      const url = `https://picsum.photos/v2/list?page=${this.page}&limit=${this.perPage}`;
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
      this.page = page;
    }
  },
  watch: {
    page() {
      this.getImages();
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
