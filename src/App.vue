<template>
  <div class="app">
    <h2>My Cats App!</h2>
    <cats-collection />
    <button @click="settings = {...settings, catsSearchApi: ''}">Change Props</button>
  </div>
</template>

<script>
  import CatsCollection from './components/CatsCollection';
  const { computed } = require('vue');

export default {
  name: 'App',
  data() {
    return {
      settings: {
        catsApiKey: 'e8d29058-baa0-4fbd-b5c2-3fa67b13b0d8',
        catsSearchApi: 'https://api.thecatapi.com/v1/images/search',
      }
    };
  },
  components: {
    'cats-collection': CatsCollection,
  },
  provide() {
    return {
      settings: computed(() => ({...this.settings }))
    }
  },
  beforeUpdate() {
    console.log('In App', this.settings)
  }
};
</script>

<style lang="scss">
.app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin: 60px auto;
  width: 100%;
  max-width: 600px;
  padding: 20px 0;
  background: #00FFFF;
  border-radius: 5px 5px 0 0 ;

  button {
    background: lightblue;
    padding: 10px;
    margin: 10px 0;
    border-radius: 5px;
    outline: 0;
  }
}
</style>
