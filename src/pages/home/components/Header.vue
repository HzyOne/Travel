<template>
    <div class="header">
        <div class="header-left">
            <div class="iconfont back-icon">&#xe743;</div>
        </div>
        <div class="header-input">
            <span class="iconfont select-icon">&#xe7b3;</span>
            请输入城市/景点/旅游主题
        </div>
        <router-link to="/city">
            <div class="header-right">
                {{this.city}}
                <span class="iconfont arrow-icon">&#xe602;</span>
            </div>
        </router-link>
    </div>
</template>

<script>
import { mapState } from 'vuex'
export default {
  name: 'HomeHeader',
  computed: {
    ...mapState(['city'])
  }
}
</script>

<style lang="stylus" scoped>
    .header
        display: flex
        height: .86rem
        line-height: .86rem
        background: #00bcd4
        color: #fff
        .header-left
            width: .64rem
            float: left
            .back-icon
                text-align: center
                font-size: .5rem
        .header-input
            flex: 1
            height: .64rem
            line-height: .64rem
            background: #fff
            border-radius: .1rem
            margin: .12rem .14rem
            padding-left: .2rem
            color: #CCC
            .select-icon
                text-align: center
                font-size: .3rem
        .header-right
            min-width: 1.04rem
            padding: 0 .1rem
            float: right
            text-align: center
            color: #fff
</style>
