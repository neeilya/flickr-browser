<template>
  <div class="img card" v-bind:style="`background-image:url('${ data.url_n }')`"></div>
</template>

<script type="text/babel">
  export default {
    props: ['data'],
  };
</script>
