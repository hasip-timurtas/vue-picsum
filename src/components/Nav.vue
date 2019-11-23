<template>
  <nav>
    <ul class="pagination">
      <li class="page__item">
        <button
          type="button"
          class="page__link"
          v-if="page != 1"
          @click="decreasePage"
        >
          Previous
        </button>
      </li>
      <li class="page__item">
        <button type="button" class="page__link">
          {{ page }}
        </button>
      </li>
      <li class="page__item">
        <button
          type="button"
          v-if="!lastPage"
          @click="increasePage"
          class="page__link"
        >
          Next
        </button>
      </li>
    </ul>
    Images Per Page:
    <select class="page__link" @change="onPerpageChange" v-model="perPage">
      <option value="30">30</option>
      <option value="50">50</option>
      <option value="75">75</option>
      <option value="100">100</option>
    </select>
  </nav>
</template>

<script>
export default {
  name: "Nav",
  props: ["page", "lastPage", "perPage"],
  data() {
    return {
      childPage: 1
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
    onPerpageChange(event) {
      this.$emit("onPerpageChange", event);
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
nav {
  margin-top: 50px;
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
