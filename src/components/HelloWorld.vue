<template>
  <v-container>
    <v-row class="text-center">
      btc usd price : {{this.price}}
    </v-row>
  </v-container>
</template>

<script>
const socketTrade = new WebSocket("wss://stream.binance.com:9443/ws/btcusdt@trade")

export default {
  name: 'HelloWorld',

  data() {
    return {
      price: ''
    }    
  },
  mounted: function() {
    socketTrade.onmessage = function(event) {      
      const binanceData = JSON.parse(event.data)
      this.price = binanceData.p
    }.bind(this)
  },
  methods: {

  }      
}
</script>
