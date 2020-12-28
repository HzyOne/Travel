<template>
    <div>
        <div class="recommend-title">
            <img class="recommend-img" src="../iconImg/hot.png" />
            <div class="recommend-text">热销推荐</div>
        </div>
        <ul>
            <router-link
                tag="li"
                class="item border-bottom"
                v-for="item of list"
                :key="item.id"
                :to="'/detail/' + item.id"
            >
                <div class="item-img-warrper">
                    <img class="item-img" :src="item.imgUrl">
                </div>
                <div class="item-info">
                    <p class="item-title">{{item.title}}</p>
                    <p class="item-desc">{{item.desc}}</p>
                    <button class="item-button">查看详情</button>
                </div>
            </router-link>
        </ul>
    </div>
</template>

<script>
export default {
  props: {
    list: Array
  },
  name: 'HomeRecommend'
}
</script>

<style lang="stylus" scoped>
    @import '../../../assets/style/mixins.styl'
    .recommend-title
        display: flex
        flex-direction: row
        align-items: center
        margin-top: .2rem
        line-height: .8rem
        background: #eee
        .recommend-img
            padding-left: .2rem
            width: .4rem
            height: .4rem
        .recommend-text
            text-align: center
            text-indent: .08rem
            letter-spacing: .04rem
    .item
        overflow: hidden
        height: 1.9rem
        display: flex
        .item-img
            width: 2.6rem
            height: 1.7rem
            padding: .1rem
        .item-info
            flex: 1
            padding: .1rem
            min-width: 0
            .item-title
                line-height: .54rem
                font-size: .32rem
                ellipsis()
            .item-desc
                height: .4rem
                line-height: .4rem
                color: #ccc
                font-size: .18rem
                ellipsis()
            .item-button
                background: #ff9300
                padding: .1rem
                margin-top: .13rem
                border-radius: .06rem
                color: #fff
</style>
