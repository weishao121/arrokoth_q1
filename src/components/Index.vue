<template>
  <div class="wrapper">
    <div v-if='data !== null'>
      <!-- <h1>{{msg}}</h1> -->
      <div class="price">
        <div class="price_card" v-for='d in data' :key='d.name'>
          <h1>{{d.name}}</h1>
          <h2>${{d.price}}</h2><span>bid: {{d.bid}}</span><span> ask: {{d.ask}}</span>
          <h2>Volume: {{d.volumeUsd24h.toFixed(2)}}</h2>
        </div>
      </div>
    </div>
    <div v-else>
      Unable to fetch data.
    </div>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  name: 'Index',
  data () {
    return {
      // msg: 'Spot price of BTC/USDT & ETH/USDT (update every 10 seconds)',
      data: null
    }
  },
  mounted () {
    this.fetchData()
    window.setInterval(() => {
      this.fetchData()
    }, 10000)
  },
  methods: {
    fetchData () {
      axios.get('https://ftx.com/api/markets')
        .then(res => {
          this.data = []
          for (let row of res.data.result) {
            if (row.type === 'spot' && (row.name === 'BTC/USDT' || row.name === 'ETH/USDT')) {
              const { name, bid, ask, price, underlying, volumeUsd24h } = row
              let newRow = {name, bid, ask, price, underlying, volumeUsd24h}
              this.data.push(newRow)
            }
          }
        })
        .catch(err => {
          console.log('Failure')
          console.log(err.message)
        })
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
body {
  margin: 0;
  font-family: 'Source Sans Pro', sans-serif;
  background-color: #f6f6f6;
}
h2 {
  font-size: 1.6rem;
}
span {
  font-size: 1.2rem;
}
.wrapper {
  padding: 0 1rem;
}
.price {
  display: -ms-grid;
  display: grid;
  -ms-grid-columns: (minmax(360px, 1fr))[auto-fill];
      grid-template-columns: repeat(auto-fill, minmax(360px, 1fr));
  grid-gap: 2rem;
}
.price_card {
  text-decoration: none;
  color: #080808;
  background-color: #fff;
  padding: 20px;
}
.price_card:hover {
  -webkit-box-shadow: 0 3px 3px rgba(0, 0, 0, 0.16), 0 3px 3px rgba(0, 0, 0, 0.23);
          box-shadow: 0 3px 3px rgba(0, 0, 0, 0.16), 0 3px 3px rgba(0, 0, 0, 0.23);
}
</style>
