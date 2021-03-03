<template>
  <v-container>
    <v-row class="text-center">
      <h1>btc usd price : {{this.price}}</h1>
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
  watch: {
    // whenever price changes, this function will run
    price: function (newPrice) {
      if (parseInt(newPrice) > 50450) {
        this.playAudio()
        console.log("toto")
        this.stopAudio()
      } else {
        console.log("tata")
      }
    }
  },
  methods: {
    playAudio() {
      const audio = new Audio('https://interactive-examples.mdn.mozilla.net/media/cc0-audio/t-rex-roar.mp3');
      audio.play();
    },
    stopAudio() {
      const audio = new Audio('https://interactive-examples.mdn.mozilla.net/media/cc0-audio/t-rex-roar.mp3');
      audio.pause();
    }
  }      
}
</script>
