<template>
  <div id="app">
    <header class="header">
      <div><h2>BTC ETH / USDT spot price (updated every 10 secs)</h2></div>
    </header>
    <router-view/>
  </div>
</template>

<script>
export default {
  name: 'App'
}
</script>

<style>

.header {
  display: -webkit-box;
  display: -ms-flexbox;
  display: flex;
  -webkit-box-pack: justify;
      -ms-flex-pack: justify;
          justify-content: space-between;
  -webkit-box-align: center;
      -ms-flex-align: center;
          align-items: center;
  padding: 10px;
  color: #fff;
  background-color: #10555A;
  margin-bottom: 10px;
}
</style>
