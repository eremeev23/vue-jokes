<template>
  <div id="app">
      <SearchBar 
      v-if="!errored"
      :jokes__arr='jokes.jokes'
      />
      <h1 v-if="errored">Ошибка отправки запроса.</h1>
  </div>
</template>

<script>
import SearchBar from '@/components/SearchBar';

export default {
  name: 'app',
  components: {
    SearchBar,
  },
  data() {
    return{
      jokes: [],
      errored: false
    }
  },
  
  created() {
    const axios = require('axios').default;
    axios
      .get('https://v2.jokeapi.dev/joke/Any?type=single&amount=10')
      .then(response => this.jokes = response.data)
      .catch(error => {
        console.log(error);
        this.errored = true;
        this.$root.log(this.jokes)
      })
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Montserrat:wght@200;400;500;600&display=swap');

* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
#app {
  font-family: 'Montserrat', sans-serif;
  font-weight: 400;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  min-height: 100vh;
  background-image: linear-gradient(to top left, #00eeff, #00b7ff);
}
h1{
  text-transform: uppercase;
}
</style>
