<template>
  <div id="app">
    
  </div>
</template>

<script>

export default {
  name: 'App',
  components: {

  },
  data() {
    return {

    }
  },
  mounted() {
    axios
    .get()
    .then()
    .catch(err => {
      console.error(err);
    })
  }
}
</script>

<style lang="scss">
#app {
  *{
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }
}
</style>
