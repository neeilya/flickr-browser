<template>
  <div class="hero navbar">
    <div class="hero-head">
      <div class="container">
        <nav class="nav">
          <div class="nav-left">
            <div class="nav-item brand">
              <a class="is-brand" target="_blank" href="https://www.smartdevs.io">SmartDevs.io</a>
            </div>
          </div>
          <div class="nav-center">
            <div class="nav-item">
              <input class="input search"
                     v-model="tag"
                     placeholder="Type to search"
                     autofocus="autofocus"
              />
            </div>
          </div>
          <div class="nav-item">
            <span class="nav-toggle"
                  v-on:click="navOpened = !navOpened"
                  v-bind:class="{ 'is-active': navOpened }"
            >
              <span></span>
              <span></span>
              <span></span>
            </span>
          </div>

          <div class="nav-right nav-menu">
            <span class="nav-item">
              <a class="button" target="_blank" href="https://github.com/neeilya">
                <span>Github</span>
              </a>
            </span>
          </div>
        </nav>
      </div>
    </div>
  </div>
</template>

<script type="text/babel">
  export default {
    data() {
      return {
        navOpened: false,
        tag: null,
      };
    },
    watch: {
      tag(val) {
        this.tag = val;
        this.$emit('tagChange', this.tag);
      },
    },
  };
</script>
