<template>
  <q-page class="flex flex-center">
    <q-banner class="bg-primary text-white text-center absolute-top">
      Saiba os valores atualizados das moedas com o CoinDesk -  https://www.coindesk.com/api
    </q-banner>
    <q-card class="text-center q-pa-lg" dark bordered style="background: radial-gradient(circle, #35a2ff 0%, #014a88 100%)">
      <q-card-title class="text-center text-h6">
        Preços de BitCoins
      </q-card-title><q-space/><q-separator/><q-space/><q-separator/>
      <q-card-main v-for="currency in info" :key="currency" class="col">
        <q-chip outline square text-color="white" class="row q-pa-sm q-mt-lg">
        {{ currency.description }}
          <q-badge color="purple" class="q-ml-sm" >
            <span v-html="currency.symbol"></span>
            {{ currency.rate_float | currencydecimal }}
          </q-badge>
        </q-chip>
      </q-card-main>
    </q-card>
  </q-page>
</template>

<style>
</style>

<script>
import axios from 'axios'

export default {
  name: 'PageIndex',
  data () {
    return {
      info: null
    }
  },
  mounted () {
    axios
      .get('https://api.coindesk.com/v1/bpi/currentprice.json')
      .then(response => (this.info = response.data.bpi))
  },
  filters: {
    currencydecimal (value) {
      return value.toFixed(2)
    }
  }
}
</script>
