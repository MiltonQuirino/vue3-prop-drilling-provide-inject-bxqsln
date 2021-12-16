<template>
  <section class="favorite-cat">
   <p>Favorite Cat {{ index }}</p>
   <img v-if="image.url" :src="image.url" alt="Cat" />
  </section>
</template>

<script>
  import axios from 'axios';

  export default {
    name: 'CatsCollection',
    inject: ['settings'],
    data() {
      return {
        image: { url: ""} 
      };
    },
    props: {
      index: {
        type: Number,
        default: 1,
      },
    },
    watch: {
      'settings.value': function(newSettings, oldSettings) {
        if (!newSettings) return;
        this.loadNextImage();
      },
    },
    mounted() {
      this.loadNextImage();
    },
    beforeUpdate() {
      console.log('In FavoriteCat', this.settings.value);
    },
    methods: {
      async loadNextImage() {
        try {
          const { catsApiKey, catsSearchApi } = this.settings.value;

          axios.defaults.headers.common['x-api-key'] = catsApiKey;

          let response = await axios.get(catsSearchApi, { params: { limit:1, size:"full" } } );
          this.image = response.data[0];
        } catch(err) {
            console.log(err)
        }
      },
    }
  };
</script>

<style lang="scss" scoped>
  .favorite-cat {
    img {
      max-width: 200px;
      border-radius: 5px;
    }
  }
</style>