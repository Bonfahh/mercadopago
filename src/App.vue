<template>
  <div id="app">
    <img src="./assets/logo.png">
    <HelloWorld/>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld'

export default {
  name: 'App',
  components: {
    HelloWorld
  },
  beforeCreate () {
    const mercadopago = require('mercadopago');
    mercadopago.configure({
      client_id: '544664266032005',
      client_secret: 'i2NH22zM1qT56cDDVNcWzx0giIeXLv7m'
    });
    let preference = {
      items: [
        {
          id: '1',
          title: 'Practical Silk Clock',
          quantity: 10,
          currency_id: 'BRL',
          unit_price: 0.65
        }
      ],
      payer: {
        email: 'velda@gmail.com'
      }
    };

    mercadopago.preferences.create(preference)
      .then(function (preference) {
        console.log(preference)
      }).catch(function (error) {
      console.log(error)
    });
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
