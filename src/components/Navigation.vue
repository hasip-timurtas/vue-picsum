<template>
  <nav class="pagination">
    <ul>
      <li>
        <button class="button light__color" v-if="page != 1" @click="decreasePage">Prev</button>
      </li>
      <li>
        <button class="button dark__color" disabled>{{ page }}</button>
      </li>
      <li>
        <button v-if="!lastPage" @click="increasePage" class="button light__color">Next</button>
      </li>
    </ul>
    <label for="select-per-page">Images Per Page:</label>
    <select
      id="select-per-page"
      class="button light__color"
      @change="onPerPageChange"
      v-model="perPage"
    >
      <option value="30">30</option>
      <option value="50">50</option>
      <option value="75">75</option>
      <option value="100">100</option>
    </select>
  </nav>
</template>

<script>
export default {
  name: "Navigation",
  props: {
    page: {
      type: Number,
      required: true,
      default: 1
    },
    lastPage: {
      type: Boolean,
      required: true,
      default: false
    },
    perPage: {
      type: Number,
      required: true,
      default: 30
    }
  },
  data() {
    return {
      childPage: this.page
    };
  },
  methods: {
    increasePage: function() {
      this.childPage++;
      this.$emit("updatePage", this.childPage);
    },
    decreasePage: function() {
      this.childPage--;
      this.$emit("updatePage", this.childPage);
    },
    onPerPageChange(event) {
      this.$emit("onPerPageChange", event);
    }
  },
  watch: {
    page() {
      this.childPage = this.page;
    }
  }
};
</script>

<style lang="scss" scoped>
.pagination {
  margin: 50px 0 25px 0;
  height: 50px;
  width: 500px;
}
.dark__color {
  background-color: #2c3e50;
}
.light__color {
  background-color: #41b883;
}
.button {
  border: none;
  color: white;
  padding: 15px 15px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  font-size: 13px;
  cursor: pointer;
}
</style>
