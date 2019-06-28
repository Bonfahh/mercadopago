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
    // eslint-disable-next-line no-console
    console.log(mercadopago.payment);
    mercadopago.configure({
      sandbox: true,
      access_token: 'APP_USR-544664266032005-062710-65e2e43918c5bd359d324a6af50f048b-249745771'
    });
    let preference = {
      items: [
        {
          id: '1234',
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
