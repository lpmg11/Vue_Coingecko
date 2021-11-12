<template>
  <div class="container">
    <div class="row">
      <h1>Hello World</h1>
      <table class="table table-dark">
        <thead>
          <tr>
            <th v-for="title in titles" :key="title">
              {{ title }}
            </th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(coin, index) in coins" :key="coin.id">
            <td class="text-muted">
              {{ index + 1 }}
            </td>
            <td>
              <img :src="coin.image" style="width:1.5rem" class="me-2">
              <span class="me-2">
                {{ coin.name }}
              </span>
              <span class="me-2 text-uppercase text-muted">
                {{ coin.symbol }}
              </span>
            </td>
            <td>
              {{ coin.current_price }}
            </td>
            <td>
              <span v-if="coin.price_change_percentage_24h >= 0" class="text-success">
                % {{ coin.price_change_percentage_24h }}
              </span>
              <span v-else class="text-danger">
                % {{ coin.price_change_percentage_24h }}
              </span>
            </td>
            <td>
              {{ coin.total_volume }}
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script>
export default {
  name: 'App',
  data(){
    return{
      coins: [],
      titles: ["#","Coin","Price","Price Change","24h Volume"]
    }
  },
  async mounted(){
    let res = await fetch('https://api.coingecko.com/api/v3/coins/markets?vs_currency=usd&order=market_cap_desc&per_page=100&page=1&sparkline=false')
    let data = await res.json()
    console.log( data )
    this.coins = data
  },
}
</script>

<style>
</style>
