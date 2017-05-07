<template>
    <div>
      <navbar @tagChange="onTagChange" />
    </div>
</template>

<script>
  import Navbar from './components/Navbar.vue';

  export default {
    components: {
      Navbar,
    },
    methods: {
      onTagChange() {
        //
      },
    },
  };
</script>

<style lang="sass">
    @import './assets/app.sass'
</style>
