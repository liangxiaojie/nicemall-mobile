<template>
  <div class="warp-container">
    <nuxt/>
  </div>
</template>

<script>
export default {
  head () {
    return {
      meta: [{
          name: 'viewport',
          content: 'width=device-width,initial-scale=1.0,minimum-scale=1.0,maximum-scale=1.0,user-scalable=no'
        }]
    }
  },
  async beforeMount() {
    if (!this.$store.getters.user) {
      await this.$store.dispatch('getWxUserinfo');
    }
  }
}
</script>


<style>
html {
  font-family: "Source Sans Pro", -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif;
  font-size: 100px;
  word-spacing: 1px;
  -ms-text-size-adjust: 100%;
  -webkit-text-size-adjust: 100%;
  -moz-osx-font-smoothing: grayscale;
  -webkit-font-smoothing: antialiased;
  box-sizing: border-box;
}
*, *:before, *:after {
  box-sizing: border-box;
  margin: 0;
}

body {
  background-color: rgb(245, 245, 245);
}

.warp-container {
  position: relative;
  height: 100%;
  font-size: .12rem;
  margin: 0 auto;
}

@media screen and (min-width: 769px) {
  .warp-container {
    width: 768px;
  }
}

.svg-inline--fa {
  width: .18rem;
}

.divider_line {
  height: .08rem;
  background-color: rgb(245, 245, 245);
}
</style>
