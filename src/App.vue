<template>
  <div id="app">
    <div id="title">
      <img id="certain" alt="certain logo" src="./assets/certain.jpg">
      <img id="canary" alt="housecanary logo" src="./assets/house-canary.png">
    </div>
    <section v-if="error">
      <p>Unable to load data.</p>
    </section>
    <section v-else>
      <div v-if ="loading"> 
        <h2>Loading...</h2>
      </div>
      <div v-else>
        <Tables :data="property" />
      </div>
    </section>
  </div>
</template>

<script>
  import Tables from './components/Tables.vue'
  import axios from 'axios';
  import {keys} from '../keys.js'
  
  export default {
    name: 'app',
    components: {
      Tables
    },
    data(){
      return{
        property: {},
        loading: true,
        error: false,
      }
    },
    mounted(){
      let token = keys.hc_api_key;
      let secret = keys.hc_api_secret;
      let config = {  
        auth: {
          username: token,
          password: secret
        },
      };
      axios.get('https://cors-anywhere.herokuapp.com/https://api.housecanary.com/v2/property/details?address=2100+Broadway&zipcode=94115', config)
      .then(response => {
        this.property = response.data[0];
      })
      .catch(error => {
        console.error(error);
        this.error = true;
      }).finally(() => this.loading = false)
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

  #title {
    margin: auto;
  }

  #canary {
    height: 200px;
    width: 400px;
  }
</style>
