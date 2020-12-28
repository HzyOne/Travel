<template>
    <div class="list" ref="wrapper">
        <div>
            <div class="area">
                <div class="title border-topbottom">当前城市</div>
                <div class="botton-list">
                    <div class="button">{{this.currentCity}}</div>
                </div>
            </div>
            <div class="area">
                <div class="title border-topbottom">热门城市</div>
                <div class="botton-list">
                    <div
                        class="botton-wrapper"
                        v-for="item of hot"
                        :key="item.id"
                        @click="handleCityClick(item.name)"
                    >
                        <div class="button">{{item.name}}</div>
                    </div>
                </div>
            </div>
            <div
                class="area"
                v-for="(item, key) of cities"
                :key="key"
                :ref="key"
            >
                <div class="title border-topbottom">{{key}}</div>
                <div class="item-list">
                    <div
                        class="item border-bottom"
                        v-for="innerItem of item"
                        :key="innerItem.id"
                        @click="handleCityClick(innerItem.name)"
                    >
                        {{innerItem.name}}
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import { mapState } from 'vuex'
import Bscroll from 'better-scroll'
export default {
  name: 'CityList',
  props: {
    hot: Array,
    cities: Object,
    letter: String
    // 接受City父组件传来的字符串，内容为Alphabet组件传给父组件的点击哪个字母
  },
  computed: {
    ...mapState({
      currentCity: 'city'
    })
  },
  methods: {
    handleCityClick (city) {
      // this.$store.dispatch('changeCity', city)
      // 组件通过调用actions方法再执行mutations方法修改state里面的值
      this.$store.commit('changeCity', city)
      // 通过组件直接调用mutations方法修改state里面的值
      this.$router.push('/')
    }
  },
  mounted () {
    this.scroll = new Bscroll(this.$refs.wrapper, {
      click: true
    })
  },
  // 监听点击的字母列表事件
  watch: {
    letter () {
      if (this.letter) {
        const element = this.$refs[this.letter][0]
        // this.$refs[this.letter]为一个数组，其下标为0的才是DOM节点
        this.scroll.scrollToElement(element)
        // 显示对应的字母城市 element为对应的DOM节点
      }
    }
  },
  updated () {
    this.scroll.refresh()
    // 修复Bscroll插件不能滚动的问题
  }
}
</script>

<style lang="stylus" scoped>
    .border-topbottom
        &:before
            border-color: #ccc
        &:after
            border-color: #ccc
    .border-bottom
        &:before
            border-color: #ccc
    .list
        overflow: hidden
        position: absolute
        top: 1.58rem
        left: 0
        right: 0
        bottom: 0
        .title
            line-height: .44rem
            background: #eee
            padding-left: .2rem
            font-size: .26rem
            color: #666
        .botton-list
            overflow: hidden
            padding: .1rem .6rem .1rem .1rem
            .button
                width: 27%
                float: left
                margin: .1rem
                padding: .1rem 0
                text-align: center
                border: .02rem solid #ccc
                border-radius: .06rem
        .item-list
            .item
                line-height: .76rem
                color: #666
                padding-left: .2rem
</style>
