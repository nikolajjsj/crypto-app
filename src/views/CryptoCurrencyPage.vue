<template>
  <div v-if="cryptoData">
    <h1>{{ $route.params.id }}</h1>
    <CryptoChart v-if="pricesArray" :cryptoData="pricesArray" :labels="labelsArray" />
    <button class="crypto-page__back-button" @click="$router.go(-1)">Back</button>
  </div>
</template>

<script>
import CryptoChart from '../components/CryptoChart.vue'

export default {
  name: 'CryptoPage',
  components: {
    CryptoChart
  },
  data () {
    return { cryptoData: null }
  },
  async created () {
    await this.fetchCrypto()
  },
  methods: {
    async fetchCrypto () {
      try {
        const res = await fetch(
          `https://api.coingecko.com/api/v3/coins/${this.$route.params.id}/market_chart?vs_currency=usd&days=7`
        )
        this.cryptoData = await res.json()
      } catch (error) {
        console.log(error)
      }
    }
  },
  computed: {
    pricesArray: function () {
      const data = this.cryptoData.prices.map(point => point[1])
      return data
    },
    labelsArray: function () {
      const days = ['Sunday', 'Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday', 'Saturday']
      const data = this.cryptoData.prices.map(point => {
        const dayNumber = new Date(point[0]).getDay()
        return `${days[dayNumber]} - ${new Date(point[0]).getHours()}.00`
      })
      return data
    }
  }
}
</script>

<style>
.crypto-page__back-button {
  position: absolute;
  right: 1em;
  bottom: 1em;
  color: white;
  background: #2c3e50;
  height: 3em;
  width: 3em;
  border-radius: 50%;
  font-size: 1.5em;
  border: none;
  box-shadow: rgba(99, 99, 99, 0.2) 0px 2px 8px 0px;
}
</style>
