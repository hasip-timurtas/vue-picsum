<template>
  <div id="app">
    <div class="row">
      <div class="col" v-for="p in images" :key="p.id">
        <div>
          <img :src="'https://picsum.photos/id/' + p.id + '/367/267'" alt="" />
        </div>

        <div class="container">
          <h4>
            <b>{{ p.author }}</b>
          </h4>
          <p>#{{ p.id }}</p>
        </div>
      </div>
    </div>
    <nav aria-label="Page navigation example">
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
            @click="page++"
            v-if="page < pages.length"
            class="page__link"
          >
            Next
          </button>
        </li>
      </ul>
      <select @change="onPerpageChange">
        <option value="30">30</option>
        <option value="40">40</option>
        <option value="50">50</option>
        <option value="60">60</option>
        <option value="70">70</option>
        <option value="80">80</option>
        <option value="90">90</option>
        <option value="100">100</option>
      </select>
    </nav>
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
      currentPage: 1
    };
  },
  methods: {
    getImages() {
      const url = `https://picsum.photos/v2/list?page=${this.page}&limit=${this.perPage}`;
      axios
        .get(url)
        .then((res) => {
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
  },
  created() {
    this.getImages();
  }
};
</script>

<style scoped>
button.page__link {
  display: inline-block;
}
button.page__link {
  font-size: 20px;
  color: #29b3ed;
  font-weight: 500;
}

.container {
  padding: 2px 16px;
}

.card__container {
  display: flex;
  flex-wrap: wrap;
}

.row {
  display: flex;
  flex-wrap: wrap;
}

.col {
  flex: 1 0 20%;
  margin: 5px;
  align-items: center;
  justify-content: center;
}

.col img {
  width: 367px;
  height: 267px;
}
</style>
