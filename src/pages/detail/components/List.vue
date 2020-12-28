<template>
    <div>
        <div
            class="item"
            v-for="(item, index) of list"
            :key="index"
        >
            <div class="item-title border-bottom">
                <span class="item-title-icon"></span>
                {{item.title}}
            </div>
            <div
                class="item-children"
                v-if="item.children">
                <detail-list :list="item.children"></detail-list>
            </div>
        </div>
    </div>
</template>

<script>
export default {
  name: 'DetailList',
  props: {
    list: Array
  }
}
</script>

<style lang="stylus" scoped>
    .item-title
        line-height: .8rem
        font-size: .32rem
        padding: 0 .2rem
        .item-title-icon
            position: relative
            top: .1rem
            display: inline-block
            width: .5rem
            height: .5rem
            background: url(../../../../static/images/iconImg/menpiao.png) 0 .1rem no-repeat
            margin-right: .1rem
            background-size: .4rem .36rem
    .item-children
        padding: 0 .2rem
</style>
