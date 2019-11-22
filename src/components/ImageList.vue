<template>
  <div>
    <nav>
      <ul class="pagination">
        <li class="page__item">
          <button
            type="button"
            class="page__link"
            v-if="page != 1"
            @click="page--"
          >
            Previous
          </button>
        </li>
        <li class="page__item">
          <button type="button" class="page__link" @click="page">
            {{ page }}
          </button>
        </li>
        <li class="page__item">
          <button
            type="button"
            v-if="!lastPage"
            @click="page++"
            class="page__link"
          >
            Next
          </button>
        </li>
      </ul>
      Images Per Page:
      <select class="page__link" @change="onPerpageChange">
        <option value="30">30</option>
        <option value="50">50</option>
        <option value="75">75</option>
        <option value="100">100</option>
      </select>
    </nav>

    <div class="row">
      <div class="col" v-for="p in images" :key="p.id">
        <a :href="p.url" target="_blank">
          <img :src="'https://picsum.photos/id/' + p.id + '/367/267'" alt="" />
        </a>
        <div class="container">
          <h4>
            <b>{{ p.author }}</b>
          </h4>
          <p>#{{ p.id }}</p>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import axios from "axios";
export default {
  name: "ImageList",
  data() {
    return {
      images: [""],
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
}

nav {
  height: 50px;
  width: 450px;
}

.page__link {
  font-size: 20px;
  color: #2c3e50;
  font-weight: 500;
  display: inline-block;
  background-color: #ffffff;
}
</style>
