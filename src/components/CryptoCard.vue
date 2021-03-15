<template>
  <div class="crypto-card" @click="$router.push({ name: 'CryptoPage', params: { id: cryptoData.id } })">
    <div class="crypto-card__head">
      <span class="crypto-card__rank">{{ cryptoData.market_cap_rank }}</span>
      <img class="crypto-card__icon" :src="cryptoData.image" alt="Cryptocurrency icon" />
      <h3 class="crypto-card__title">{{ cryptoData.name }} ({{ cryptoData.symbol }})</h3>
    </div>
    <div class="crypto-card__details">
      <h4 :class="classObject">{{ dailyChange }}%</h4>
      <h4 class="crypto-card__price">{{ currentPrice }}$</h4>
    </div>
  </div>
</template>

<script>
import { currencyFormatter } from '@/helper/Formatter.js'

export default {
  name: 'CryptoCard',
  props: {
    cryptoData: {
      type: Object,
      required: true
    }
  },
  computed: {
    dailyChange: function () {
      return (Math.round(this.cryptoData.market_cap_change_percentage_24h * 100) / 100).toFixed(2)
    },
    currentPrice: function () {
      return currencyFormatter.format(this.cryptoData.current_price)
    },
    classObject: function () {
      return {
        'crypto-card__price-change': true,
        'text-danger': `${this.cryptoData.market_cap_change_percentage_24h}`.startsWith('-'),
        'text-succes': !`${this.cryptoData.market_cap_change_percentage_24h}`.startsWith('-')
      }
    }
  }
}
</script>

<style scoped>
.crypto-card {
  width: 80%;
  margin: 1em auto;
  box-shadow: rgba(0, 0, 0, 0.24) 0px 3px 8px;
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 1em;
  cursor: pointer;
  transition: 0.2s;
}

.crypto-card > * {
  display: flex;
  align-items: center;
}

.crypto-card > * > * {
  margin: .5em;
}

.crypto-card:hover {
  box-shadow: rgba(0, 0, 0, 0.44) 0px 3px 8px;
  transform: scale(1.05);
}

.crypto-card__rank {
  font-weight: bolder;
}

.crypto-card__title {
  font-size: 1.25em;
}

.crypto-card__icon {
  height: 2em;
  width: 2em;
}
</style>
