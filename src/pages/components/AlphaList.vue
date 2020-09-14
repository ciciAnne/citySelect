<template>
  <ul class="list" ref="list">
    <li class="item" v-for="(item, key) in alphalist" :key="key" @touchstart="handleStart" @touchmove="handleMove">{{item}}</li>
  </ul>
</template>

<script>
export default{
  name: 'CityList',
  props: {
    alphalist: Array
  },
  data () {
    return {
      timer: null
    }
  },
  computed: {
    letterATop () {
      return this.$refs.list.offsetTop
    }
  },
  methods: {
    handleStart (e) {
      this.$emit('handleEle', e.target.innerText)
    },
    handleMove (e) {
      if (this.timer) {
        clearTimeout(this.timer)
      }
      this.timer = setTimeout(() => {
        let index = Math.floor((e.touches[0].clientY - this.letterATop) / 20) // 计算出第几位字母
        this.$emit('handleEle', this.alphalist[index])
        console.log(this.alphalist[index])
      }, 200)
    }
  }
}
</script>

<style scoped>
  .list{
    position: fixed;
    right: 0;
    top: 200px;
    z-index: 1;
    width: .6rem;
  }
  .item{
    line-height: .4rem;
    text-align: center;
  }
</style>
