<template>
  <input
    v-model="searchText"
    type="text"
    class="home-search-input"
    placeholder="Pesquisar"
  />
</template>

<script>
export default {
  data: () => ({
    searchText: "",
  }),
  watch: {
    searchText() {
      this.$emit("onSearchChange", this.searchText);
    },
  },
};
</script>

<style scoped>
.home-search-input {
  width: 100%;
  height: 40px;
  border: none;
  border-radius: 8px;
  outline: none;
  padding: 4px 20px;
  background: #aaaaaa;
  margin-bottom: 20px;
}

.home-search-input::placeholder {
  color: #000000;
}
</style>
