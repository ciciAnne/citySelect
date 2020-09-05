<template>
  <div>
    <city-header :cities="cities"></city-header>
    <city-list :cities="cities" :hotCities="hotCities" :ele="ele"></city-list>
    <alpha-list :alphalist="alphalist" v-on:handleEle="handleEle"></alpha-list>
  </div>
</template>

<script>
import CityHeader from './components/Header.vue'
import CityList from './components/CityList.vue'
import AlphaList from './components/AlphaList.vue'

export default{
  name: 'City',
  components: {
    CityHeader,
    CityList,
    AlphaList
  },
  data () {
    return {
      hotCities: [],
      cities: {},
      alphalist: [],
      currentCity: '杭州',
      ele: {},
      top: 0
    }
  },
  methods: {
    handleEle (e) {
      this.ele = e
    },
    getMsg () {
      let xhr = new XMLHttpRequest()
      let _this = this
      xhr.onreadystatechange = function () {
        if (xhr.readyState === 4) {
          if ((xhr.status >= 200 && xhr.status < 300) || xhr.status === 304) {
            let msg = JSON.parse(xhr.responseText)
            if (msg.ret) {
              _this.hotCities = msg.data.hotCities
              _this.cities = msg.data.cities
              _this.alphalist = []
              for (var key in _this.cities) {
                _this.alphalist.push(key)
              }
            }
          } else {
            alert('发生错误：' + xhr.status)
          }
        }
      }
      xhr.open('get', '../../static/mock/city.json', true)
      xhr.send(null)
    }
  },
  mounted () {
    this.getMsg()
  }
}
</script>

<style scoped>
</style>
