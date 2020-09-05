<template>
  <router-link to="/city">
    <div class="city">
      当前城市:{{this.city}}
    </div>
  </router-link>
</template>

<script>
export default {
  name: 'Index',
  computed: {
    city () {
      return this.$store.state.city
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .city{
    color: #000;
  }
  a{
    text-decoration: none;
  }
</style>
