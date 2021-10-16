<template>
  <b-row class="m-3">
    <b-col md="4" offset-md="4">
      <b-form-input
        v-model="search"
        @input="searchChangeHandler"
        class="text-light shadow-none input"
        placeholder="Search"
      ></b-form-input>
    </b-col>
  </b-row>
</template>

<script>
export default {
  emits: ["search-change"],
  data() {
    return {
      search: "",
    };
  },
  methods: {
    searchChangeHandler() {
      this.$emit("search-change", this.search);
    },
  },
};
</script>

<style scoped>
.input {
  border-radius: 4px;
  border: none;
  background-image: linear-gradient(
    -225deg,
    #ac32e4 0%,
    #7918f2 48%,
    #4801ff 100%
  );
}
.input::placeholder {
  color: #fff;
}
</style>
