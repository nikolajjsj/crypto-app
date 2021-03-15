<template>
  <div class="home">
    <CryptoCard v-for="crypto in marketData" :key="crypto.id" :cryptoData="crypto" />
  </div>
</template>

<script>
import CryptoCard from '@/components/CryptoCard.vue'

export default {
  name: 'Home',
  components: {
    CryptoCard
  },
  data () {
    return {
      marketData: null
    }
  },
  async created () {
    await this.fetchCryptoMarket()
  },
  methods: {
    async fetchCryptoMarket () {
      try {
        const res = await fetch(
          'https://api.coingecko.com/api/v3/coins/markets?vs_currency=usd&order=market_cap_desc&per_page=100&page=1&sparkline=false'
        )
        const jsonData = await res.json()
        this.marketData = jsonData
        console.log(jsonData)
      } catch (error) {
        print(error)
      }
    }
  }
}
</script>
