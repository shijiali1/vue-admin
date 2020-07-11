<template>
  <div class="dashboard-container">
    <div class="dashboard-text">name: {{ name }}</div>
    <!-- <a id="btnTop" class="btnTop" href="javascript:;" title="Back to top"> -->
    <!-- <img src="../../assets/404_images/back.png" class="imageTop"> -->
    <img v-if="btnFlag" class="imageTop" src="../../assets/404_images/back.png" @click="backTop">
    <!-- </a> -->
  </div>
</template>

<script>
import { mapGetters } from 'vuex'

export default {
  name: 'Dashboard',
  computed: {
    ...mapGetters([
      'name'
    ])
  },
  data() {
    return {
      btnFlag: false
    }
  },
  watch: {

  },
  mounted() {
    window.addEventListener('scroll', this.scrollToTop)
  },
  destroyed() {
    window.removeEventListener('scroll', this.scrollToTop)
  },
  methods: {
    // 点击图片回到顶部方法，加计时器是为了过渡顺滑
    backTop() {
      const that = this
      const timer = setInterval(() => {
        const ispeed = Math.floor(-that.scrollTop / 5)
        document.documentElement.scrollTop = document.body.scrollTop = that.scrollTop + ispeed
        if (that.scrollTop === 0) {
          clearInterval(timer)
        }
      }, 16)
    },

    // 为了计算距离顶部的高度，当高度大于60显示回顶部图标，小于60则隐藏
    scrollToTop() {
      const that = this
      const scrollTop = window.pageYOffset || document.documentElement.scrollTop || document.body.scrollTop
      that.scrollTop = scrollTop
      if (that.scrollTop > 0) {
        that.btnFlag = true
      } else {
        that.btnFlag = false
      }
    }

  }
}
</script>

<style lang="scss" scoped>
.dashboard-container{
  height: 1200px;
}
  // .btnTop { position: fixed; right: 2%; bottom: 2%; cursor: pointer; opacity: .7; z-index: 9; }
.imageTop:hover { opacity: 1;}
.imageTop { width: 72px;position: fixed; right: 2%; bottom: 2%; cursor: pointer; opacity: 0.7; z-index: 9;}
.dashboard {

  &-container {
    margin: 30px;
  }
  &-text {
    font-size: 30px;
    line-height: 46px;
  }
}
</style>
