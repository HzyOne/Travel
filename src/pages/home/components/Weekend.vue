<template>
    <div>
        <div class="weekend-title">
            <img class="weekend-img" src="../iconImg/play.png" />
            <div class="weekend-text">周末去哪儿</div>
        </div>
        <ul>
            <li v-for="item of list"
                :key="item.id"
            >
                <div class="item-img-warrper">
                    <img class="item-img" :src="item.imgUrl">
                </div>
                <div class="item-info">
                    <p class="item-title">{{item.title}}</p>
                    <p class="item-desc">{{item.desc}}</p>
                </div>
            </li>
        </ul>
    </div>
</template>

<script>
export default {
  props: {
    list: Array
  },
  name: 'HomeWeekend'
}
</script>

<style lang="stylus" scoped>
    @import '../../../assets/style/mixins.styl'
    .weekend-title
        display: flex
        flex-direction: row
        align-items: center
        line-height: .8rem
        background: #eee
        .weekend-img
            padding-left: .2rem
            width: .4rem
            height: .4rem
        .weekend-text
            text-align: center
            text-indent: .08rem
            letter-spacing: .04rem
    .item-img-warrper
        height: 0
        overflow: hidden
        padding-bottom: 36.65%
        .item-img
            width: 100%
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
            color: #333
            font-size: .18rem
            ellipsis()
</style>
