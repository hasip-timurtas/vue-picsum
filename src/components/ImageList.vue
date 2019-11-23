<template>
  <div>
    <Nav
      :page="page"
      :lastPage="lastPage"
      :perPage="perPage"
      @updatePage="updatePage"
      @onPerpageChange="onPerpageChange"
    />
    <div class="row">
      <div class="col" v-for="p in images" :key="p.id">
        <img
          :url="p.url"
          :src="'https://picsum.photos/id/' + p.id + '/367/267'"
          alt=""
          @click="onImageClick"
        />

        <div class="container">
          <h4>
            <b>{{ p.author }}</b>
          </h4>
          <p>#{{ p.id }}</p>
        </div>
      </div>
    </div>
    <Nav
      :page="page"
      :lastPage="lastPage"
      :perPage="perPage"
      @updatePage="updatePage"
      @onPerpageChange="onPerpageChange"
    />
    <modal name="picsum-modal" width="80%" height="80%">
      <iframe
        name="picsum-frame"
        :src="selectedImageUrl"
        width="100%"
        height="100%"
      />
    </modal>
  </div>
</template>
<script>
import axios from "axios";
import Nav from "./Nav.vue";
export default {
  name: "ImageList",
  components: {
    Nav
  },
  data() {
    return {
      images: [""],
      selectedImageUrl: "",
      page: 1,
      perPage: 30,
      pages: [],
      lastPage: false
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
        .then((res) => {
          this.lastPage = res.data.length < this.perPage;
          this.images = res.data;
        })
        .catch((e) => {
          // eslint-disable-next-line no-console
          console.log(e);
        });
    },
    onImageClick(event) {
      const imgElement = event.currentTarget;
      const url = imgElement.getAttribute("url");
      const byPassFrameUrl = "https://jsonp.afeld.me/?url=";
      this.selectedImageUrl = byPassFrameUrl + url;
      this.$modal.show("picsum-modal");
    },
    setPages() {
      let numberOfPages = 10;
      for (let index = 1; index <= numberOfPages; index++) {
        this.pages.push(index);
      }
    },
    paginate(images) {
      let page = this.page;
      let perPage = this.perPage;
      let from = page * perPage - perPage;
      let to = page * perPage;
      return images.slice(from, to);
    },
    onPerpageChange(event) {
      this.perPage = event.target.value;
    },
    updatePage(page) {
      this.page = page;
    }
  },
  watch: {
    images() {
      this.setPages();
    },
    page() {
      this.getImages();
    },
    perPage() {
      this.getImages();
    }
  }
};
</script>

<style scoped>
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
