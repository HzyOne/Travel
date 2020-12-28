<template>
    <div>
        <div class="search">
            <input
                v-model="keyword"
                class="search-input"
                type="text"
                placeholder="请输入城市名或拼音"
            />
        </div>
        <div
            class="search-content"
            ref="search"
            v-show="keyword"
        >
            <ul>
                <li
                    class="serach-item border-bottom"
                    v-for="item of list"
                    :key="item.id"
                    @click="handleCityClick(item.name)"
                >
                    {{item.name}}
                </li>
                <li
                    class="serach-item border-bottom"
                    v-show="hasNoData">
                    没有找到匹配数据
                </li>
            </ul>
        </div>
    </div>
</template>

<script>
import Bscroll from 'better-scroll'
export default {
  name: 'CitySearch',
  props: {
    cities: Object
  },
  data () {
    return {
      keyword: '',
      list: [],
      timer: null
    }
  },
  computed: {
    hasNoData () {
      return !this.list.length
    }
  },
  watch: {
    keyword () {
      if (this.timer) {
        clearTimeout(this.timer)
      }
      if (!this.keyword) {
        this.list = []
        return
      }
      this.timer = setTimeout(() => {
        const result = []
        for (let i in this.cities) {
          this.cities[i].forEach((value) => {
            if (value.spell.indexOf(this.keyword) > -1 || value.name.indexOf(this.keyword) > -1) {
              result.push(value)
            }
          })
        }
        // 将city.json文件中的cities数据的“key”（字母）值循环后存入i变量中
        // 然后对“key”（字母）中的值进行循环存入value中，此时的value中的数据为：{id:"001",spell:"biejin",...}
        // 再对value中的值进行一个判断，如果与绑定的数据keyword（输入的值）中有相同的字符或字符串，即value中的spell和name的值
        // 将与keyword值相同的vlaue对象添加到result数组中
        this.list = result
        // 将result数组赋值给data数据里面的list空数组
      }, 100)
    }
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
    this.scroll = new Bscroll(this.$refs.search)
  },
  updated () {
    this.scroll.refresh()
    // 修复Bscroll插件不能滚动的问题
  }
}
</script>

<style lang="stylus" scoped>
    .search
        height: .72rem
        line-height: .72rem
        padding: 0 .12rem
        background: #00bcd4
        .search-input
            box-sizing: border-box
            width: 100%
            height: .62rem
            line-height: .62rem
            padding: 0 .1rem
            text-align: center
            border-radius: .06rem
            color: #666
    .search-content
        overflow: hidden
        position: absolute
        z-index: 1
        top:1.58rem
        left: 0
        right: 0
        bottom: 0
        background: #eee
        .serach-item
            line-height: .62rem
            padding-left: .2rem
            color: #666
            background: #fff
</style>
