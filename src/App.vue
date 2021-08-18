<template>
  <div id="app">
      <SearchBar />
      <ListItem 
      :jokes__list='jokes.data.jokes'
      />
  </div>
</template>

<script>
import SearchBar from '@/components/SearchBar';
import ListItem from '@/components/ListItem';


export default {
  name: 'app',
  components: {
    SearchBar,
    ListItem
  },
  data() {
    return{
      jokes: null
    }
  },
  
  mounted() {
    const axios = require('axios').default;
    axios
      .get('https://v2.jokeapi.dev/joke/Any?type=single&amount=10')
      .then(response => this.jokes = response)
  }
}
</script>

<style>
@font-face {
    font-family: 'Bw Modelica';
    src:url('./assets/BwModelicaCyrillicDEMO-Medium.woff2') format('woff2'),
        url('./assets/BwModelicaCyrillicDEMO-Medium.woff') format('woff'),
        url('./assets/BwModelicaCyrillicDEMO-Medium.ttf') format('truetype');
    font-weight: 500;
    font-style: normal;
}
@font-face {
    font-family: 'Bw Modelica';
    src:url('./assets/BwModelicaCyrillicDEMO-ExtraBold.woff2') format('woff2'),
        url('./assets/BwModelicaCyrillicDEMO-ExtraBold.woff') format('woff'),
        url('./assets/BwModelicaCyrillicDEMO-ExtraBold.ttf') format('truetype');
    font-weight: 800;
    font-style: bold;
  }

* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
#app {
  font-family: 'Bw Modelica';
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  min-height: 100vh;
  background-image: linear-gradient(to top, #89c4ff, #349aff, #1856ff);
}
</style>
