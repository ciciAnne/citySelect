<template>
  <div class="header">
    <router-link to="/">
      <span class="iconfont back-icon">&#xe609;</span>
    </router-link>
    <span class="iconfont search-icon">&#xe616;</span><input placeholder="城市/拼音" class="search" v-model="msg">
    <div class="search-content" v-show="isSearchShow">
      <ul class="item-list">
        <li class="item" v-for="(item, key) in result" :key="key" @click="handleClick(item)">{{item}}</li>
      </ul>
      <div class="search-none" v-show="isNoneShow">未找到匹配项</div>
    </div>
  </div>
</template>

<script>
export default{
  name: 'Header',
  props: {
    cities: Object
  },
  data () {
    return {
      isSearchShow: false,
      isNoneShow: false,
      result: [],
      msg: ''
    }
  },
  watch: {
    msg () {
      this.isSearchShow = true
      this.result = []
      for (let i in this.cities) {
        this.cities[i].forEach((value) => {
          if (value.spell.indexOf(this.msg) !== -1 || value.name.indexOf(this.msg) !== -1) {
            this.result.push(value.name)
          }
        })
      }
      if (!this.msg) {
        this.isSearchShow = false
      }
      if (this.result.length === 0) {
        this.isNoneShow = true
      }
    }
  },
  methods: {
    handleClick (msg) {
      this.$store.commit('changeCity', msg)
      this.$router.push('/')
      this.isSearchShow = false
    }
  }
}
</script>

<style scoped>
  .header{
    background: #42B983;
    height: 40px;
    display: flex;
    width: 100%;
  }
  .back-icon{
    font-size: 22px;
    line-height: 40px;
    padding: 0 10px;
    margin-right: 20px;
    color: #fff;
  }
  .search-icon{
    background: #fff;
    margin: 7px -1px 7px 0;
    padding: 0 5px;
    line-height: 26px;
    border: none;
    border-top-left-radius: 5px;
    border-bottom-left-radius: 5px;
  }
  .search{
    flex: 1;
    margin: 7px 50px 7px 0;
    padding-left: 5px;
    border-top-right-radius: 5px;
    border-bottom-right-radius: 5px;
    background: #fff;
  }
  .search-content{
    z-index: 2;
    position: absolute;
    top: 40px;
    left: 0;
    bottom: 0;
    right: 0;
    background-color: #F5F5F5;
  }
  .item{
    background-color: #fff;
    border-bottom: 1px solid #E0E0E0;
    padding: 5px 15px;
    color: #3c3c3c;
    height: 30px;
    line-height: 30px;
    font-size: 16px;
  }
  .search-none{
    height: 30px;
    line-height: 30px;
    font-size: 16px;
    padding: 5px 15px;
    color: #3c3c3c;
    background-color: #fff;
  }
</style>
