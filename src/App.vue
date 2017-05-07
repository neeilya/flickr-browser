<template>
    <div>
      <navbar @tagChange="onTagChange" />
      <section class="section">
        <div class="container">
          <div v-show="!isTagEmpty && images.length > 0">
            <div v-for="image in images" class="col card">
              <feed-image v-bind:data="image" />
            </div>
          </div>
          <div v-show="isTagEmpty" class="has-text-centered">
            <div class="headline">
              <h2 class="subtitle is-2">Search for something amazing</h2>
            </div>
            <img src="static/promo.jpg">
          </div>
          <div v-if="loading" class="spinner-container">
            <i class="fa fa-spinner fa-5x fa-pulse" aria-hidden="true"></i>
          </div>
        </div>
      </section>
    </div>
</template>

<script>
  import axios from 'axios';
  import debounce from 'lodash/debounce';
  import config from '../config';
  import Navbar from './components/Navbar.vue';
  import FeedImage from './components/FeedImage.vue';

  export default {
    data() {
      return {
        images: [],
        loading: false,
        tag: null,
      };
    },
    components: {
      Navbar,
      FeedImage,
    },
    computed: {
      isTagEmpty() {
        return !this.tag || this.tag.length === 0;
      },
    },
    methods: {
      /* eslint-disable func-names */
      onTagChange: debounce(function (tag) {
        this.tag = tag;
        this.images = [];

        if (!this.isTagEmpty) {
          this.loading = true;

          this.fetchImages(this.tag).then((response) => {
            this.images = response.data.photos.photo;
            this.loading = false;
          });
        }
      }, 500),
      fetchImages(tag) {
        return axios({
          method: 'get',
          url: 'https://api.flickr.com/services/rest',
          params: {
            method: 'flickr.photos.search',
            api_key: config.api_key,
            tags: tag,
            extras: 'url_n',
            page: 1,
            format: 'json',
            nojsoncallback: 1,
            per_page: 30,
          },
        });
      },
    },
  };
</script>

<style lang="sass">
    @import './assets/app.sass'
</style>
