<template>
  <div class="container" ref="container">
    <div class="wrapper">
      <p class="current-title">当前城市</p>
      <div class="current-city">{{this.city}}</div>
    </div>
    <div class="wrapper">
      <p class="hot-title">热门城市</p>
      <ul class="city-list">
        <li class="item-city" v-for="item of hotCities" :key="item.id" @click="handleClick(item.name)">{{item.name}}</li>
      </ul>
    </div>
    <div class="area" v-for="(items, key) of cities" :key="key" :ref="key">
      <p class="alpha-title">{{key}}</p>
      <ul class="item-list" v-for="item of items" :key="item.id">
        <li class="item" @click="handleClick(item.name)">{{item.name}}</li>
      </ul>
    </div>
  </div>
</template>

<script>
export default{
  name: 'CityList',
  props: {
    hotCities: Array,
    cities: Object,
    ele: ''
  },
  data () {
    return {
      eleTop: 0
    }
  },
  methods: {
    handleClick (msg) {
      this.$store.commit('changeCity', msg)
      this.$router.push('/')
    }
  },
  watch: {
    ele () {
      this.eleTop = this.$refs[this.ele][0].offsetTop - 40
      this.$refs.container.scrollTo(0, this.eleTop)
    }
  },
  computed: {
    city () {
      return this.$store.state.city
    }
  },
  mounted () {
    this.$refs.container.style.height = window.innerHeight - 40 + 'px'
  }
}
</script>

<style scoped>
  .container{
    overflow: scroll;
  }
  .wrapper{
    box-sizing: border-box;
    background: #F5F5F5;
    width: 100%;
    font-size: 16px;
    padding: 0 0 10px 15px;
  }
  .current-title{
    color: #6E6E6E;
    height: 20px;
    line-height: 20px;
    padding: 5px 0;
  }
  .current-city{
    height: 30px;
    line-height: 30px;
    background-color: #fff;
    width: fit-content;
    padding: 0 18px;
    text-align: center;
    border-radius: 3px;
    margin-top: 5px;
  }
  .city-list::after{
    clear: both;
    display: block;
    content: "";
  }
  .hot-title{
    color: #6E6E6E;
    height: 20px;
    line-height: 20px;
    padding: 5px 0;
  }
  .item-city{
    color: #3c3c3c;
    float: left;
    height: 30px;
    line-height: 30px;
    background-color: #fff;
    width: 70px;
    text-align: center;
    border-radius: 3px;
    margin: 5px 15px 10px 0;
  }
  .alpha-title{
    color: #6E6E6E;
    height: 30px;
    line-height: 30px;
    padding: 0 13px;
    background: #F5F5F5;
    font-size: 16px;
    border-top: 1px solid #E0E0E0;
  }
  .item-list{
    padding: 0 15px;
  }
  .item{
    background-color: #fff;
    border-bottom: 1px solid #E0E0E0;
    padding: 5px 0;
    color: #3c3c3c;
    height: 30px;
    line-height: 30px;
    font-size: 16px;
  }
</style>
