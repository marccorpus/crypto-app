<template>
  <b-row v-if="coins.length === 0" class="mt-5">
    <b-col class="text-center"><h4>No currency found.</h4></b-col>
  </b-row>

  <b-table-simple v-else class="mt-5" dark hover responsive>
    <b-tbody>
      <b-tr v-for="coin in coins" :key="coin.id">
        <b-td>
          <b-img
            :src="coin.image"
            class="coin-image"
            rounded="circle"
            :alt="coin.name"
          ></b-img>
        </b-td>
        <b-td>{{ coin.name }}</b-td>
        <b-td class="coin-symbol">{{ coin.symbol }}</b-td>
        <b-td>${{ coin.price.toLocaleString() }}</b-td>
        <b-td>${{ coin.volume.toLocaleString() }}</b-td>
        <b-td
          ><span
            :class="{
              'upward-trend': coin.priceChange > 0,
              'downward-trend': coin.priceChange < 0,
            }"
            >{{ coin.priceChange.toFixed(2) }}%</span
          ></b-td
        >

        <b-td>Mkt Cap: ${{ coin.marketcap.toLocaleString() }}</b-td>
      </b-tr>
    </b-tbody>
  </b-table-simple>
</template>

<script>
export default {
  props: ["filteredCoins"],
  computed: {
    coins() {
      return this.filteredCoins.map((coin) => {
        return {
          id: coin.id,
          image: coin.image,
          name: coin.name,
          symbol: coin.symbol,
          price: coin.current_price,
          volume: coin.market_cap,
          priceChange: coin.price_change_percentage_24h,
          marketcap: coin.total_volume,
        };
      });
    },
  },
};
</script>

<style scoped>
.coin-image {
  height: 30px;
  width: 30px;
}
.coin-symbol {
  text-transform: uppercase;
}
.upward-trend {
  color: green;
}
.downward-trend {
  color: red;
}
</style>
