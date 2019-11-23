<template>
  <nav class="pagination">
    <ul>
      <li>
        <button class="button light__color" v-if="currentPage != 1" @click="decreasePage">Prev</button>
      </li>
      <li>
        <button class="button dark__color" disabled>{{ currentPage }}</button>
      </li>
      <li>
        <button v-if="!lastPage" @click="increasePage" class="button light__color">Next</button>
      </li>
    </ul>
    <label for="select-per-page">Images Per Page:</label>
    <select
      id="select-per-page"
      class="button light__color"
      v-model="childPerPage"
      @change="onPerPageChange"
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
    currentPage: {
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
      type: String,
      required: true,
      default: "30"
    }
  },
  data() {
    return {
      childCurrentPage: 1,
      childPerPage: "30"
    };
  },
  methods: {
    increasePage: function() {
      this.childCurrentPage++;
      this.$emit("update-current-page", this.childCurrentPage);
    },
    decreasePage: function() {
      this.childCurrentPage--;
      this.$emit("update-current-page", this.childCurrentPage);
    },
    onPerPageChange(event) {
      this.$emit("update-per-page", event);
    }
  },
  watch: {
    currentPage() {
      this.childPage = this.childCurrentPage;
    },
    perPage() {
      this.childPerPage = this.perPage;
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
