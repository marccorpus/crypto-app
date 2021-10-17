<template>
  <b-container>
    <b-row>
      <b-col class="text-center"><h3>Search a currency</h3></b-col>
    </b-row>

    <Search @search-change="searchChangeHandler" />

    <Loading v-if="loading" />

    <Coins v-else :filtered-coins="filteredCoins" />
  </b-container>
</template>

<script>
import axios from "axios";

import Search from "./Search.vue";
import Loading from "./Loading.vue";
import Coins from "./Coins.vue";

export default {
  data() {
    return {
      loading: false,
      coins: [],
      search: "",
    };
  },
  computed: {
    filteredCoins() {
      return this.coins.filter((coin) =>
        coin.name.toLowerCase().includes(this.search.toLowerCase())
      );
    },
  },
  methods: {
    getCoins() {
      this.loading = true;

      axios
        .get(
          "https://api.coingecko.com/api/v3/coins/markets?vs_currency=usd&order=market_cap_desc&sparkline=false"
        )
        .then((response) => {
          this.loading = false;
          this.coins = response.data;
        });
    },
    searchChangeHandler(search) {
      this.search = search;
    },
  },
  created() {
    this.getCoins();
  },
  components: {
    Search,
    Loading,
    Coins,
  },
};
</script>
