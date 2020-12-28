<template>
    <div>
        <router-link tag="div" to="/" class="header-abs">
            <div class="iconfont header-abs-back">&#xe743;</div>
        </router-link>
        <div
            class="header-fixed"
            v-show="!showAbs"
            :style="opacityStyle"
        >
            <router-link to="/">
                <div class="iconfont header-fixed-back">&#xe743;</div>
            </router-link>
            景点详情
        </div>
    </div>
</template>

<script>
export default {
  name: 'DetailHeader',
  data () {
    return {
      showAbs: true,
      opacityStyle: {
        opacity: 0
      }
    }
  },
  methods: {
    handleScroll () {
      const top = document.documentElement.scrollTop || document.body.scrollTop || window.pageYOffset
      if (top > 52) {
        let opacity = top / 140
        opacity = opacity > 1 ? 1 : opacity
        this.opacityStyle = { opacity }
        this.showAbs = false
      } else {
        this.showAbs = true
      }
    }
  },
  mounted () {
    window.addEventListener('scroll', this.handleScroll)
  },
  destroyed () {
    window.removeEventListener('scroll', this.handleScroll)
  }
}
</script>

<style lang="stylus" scoped>
    .header-abs
        position: absolute
        left: .2rem
        top: .2rem
        width: .68rem
        height: .68rem
        line-height: .68rem
        text-align: center
        border-radius: 50%
        background: rgba(0, 0, 0, .6)
        .header-abs-back
            color: #fff
            font-size: .4rem
    .header-fixed
        z-index: 2
        position: fixed
        top: 0
        left: 0
        right: 0
        overflow: hidden
        height: .86rem
        line-height: .86rem
        text-align: center
        color: #fff
        background: #00bcd4
        font-size: .32rem
        .header-fixed-back
            position: absolute
            width .64rem
            top: 0
            left: 0
            text-align: center
            font-size: .4rem
            color: #fff
</style>
