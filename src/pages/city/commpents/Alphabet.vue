<template>
    <ul class="list">
        <li
          class="item"
          v-for="item of letters"
          :key="item"
          :ref="item"
          @touchstart="handleTouchStart"
          @touchmove="handleTouchMove"
          @touchend="handleTouchEnd"
          @click="handleLetterClick"
        >
          {{item}}
        </li>
    </ul>
</template>

<script>
export default {
  name: 'CityAlphabet',
  props: {
    cities: Object
  },
  data () {
    return {
      touchStatus: false,
      startY: 0,
      timer: null
    }
  },
  updated () {
    this.startY = this.$refs['A'][0].offsetTop
  },
  computed: {
    letters () {
      const letters = []
      for (let i in this.cities) {
        letters.push(i)
      }
      return letters
    }
  },
  methods: {
    handleLetterClick (even) {
      this.$emit('change', even.target.innerText)
    },
    handleTouchStart () {
      this.touchStatus = true
    },
    handleTouchMove (even) {
      if (this.touchStatus) {
        if (this.timer) {
          clearTimeout(this.timer)
        }
        this.timer = setTimeout(() => {
          const touchY = even.touches[0].clientY - 79
          const index = Math.floor((touchY - this.startY) / 24)
          if (index >= 0 && index <= this.letters.length) {
            this.$emit('change', this.letters[index])
          }
        }, 8)
        // 在下滑字母列表的过程中，延迟8ms响应handleTouchMove函数，如在8ms内继续下滑，将会清除上一次handleTouchMove
        // 函数计算的内容，从而优化网页性能（节流）
      }
    },
    handleTouchEnd () {
      this.touchStatus = false
    }
  }
}
</script>

<style lang="stylus" scoped>
  .list
    display: flex
    flex-direction: column
    justify-content: center
    position: absolute
    top: 1.59rem
    right: 0
    bottom: 0
    width: .4rem
    .item
      line-height: .48rem
      text-align: center
      color: #00bcd4
</style>
