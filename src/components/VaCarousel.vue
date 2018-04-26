<template>
  <div class="va-carousel"
    @mouseenter.stop="handleMouseEnter"
    @mouseleave.stop="handleMouseLeave"
    :style="{ width: width, height: height}">
    <transition-group name="list"
      tag="div"
      class="image-list"
      :css="false"
      @before-enter="beforeEnter"
      @enter="enter"
      @before-leave="beforeLeave"
      @leave="leave">

      <div class="image-item"
        :style="{width: itemWidth}"
        v-for="(item, index) in list"
        :class="{active: index === (total - 1) / 2}"
        :key="item.id">
        <img :src="item.src"
          :alt="item.name"
          :style="{width: imgWidth, height: imgHeight}"
          @click="selectedItem(item, index)">
      </div>

      <template v-if="arrow === 'always' || hover">
        <span key="prev"
          class="preview"
          @click="prev">
          <slot name="prev">
            {{ prevText }}
          </slot>
        </span>

        <span key="next"
          class="next"
          @click="next">
          <slot name="next"> {{ nextText }}</slot>
        </span>
      </template>
    </transition-group>
  </div>

</template>

<script>
import Velocity from 'velocity-animate'
export default {
  name: 'VACarousel',

  props: {
    items: {
      type: Array,
      default: () => {
        return [
          { id: 1, src: '../../static/images/1.jpg' },
          { id: 2, src: '../../static/images/2.jpg' },
          { id: 3, src: '../../static/images/3.jpg' },
          { id: 4, src: '../../static/images/4.jpg' },
          { id: 5, src: '../../static/images/5.jpg' },
          { id: 6, src: '../../static/images/6.jpg' },
          { id: 7, src: '../../static/images/7.jpg' },
          { id: 8, src: '../../static/images/8.jpg' },
          { id: 9, src: '../../static/images/9.jpg' },
          { id: 10, src: '../../static/images/10.jpg' },
          { id: 11, src: '../../static/images/11.jpg' },
          { id: 12, src: '../../static/images/12.jpg' },
          { id: 13, src: '../../static/images/13.jpg' },
          { id: 14, src: '../../static/images/14.jpg' }
        ]
      }
    },
    total: {
      tyep: Number,
      default: 7
    },
    height: {
      type: String,
      default: '180px'
    },
    width: {
      type: String,
      default: '90%'
    },

    imgWidth: {
      type: String,
      default: '100%'
    },
    imgHeight: {
      type: String,
      default: '70%'
    },

    autoplay: {
      type: Boolean,
      default: true
    },
    interval: {
      type: Number,
      default: 2000
    },
    prevText: {
      type: String,
      default: 'prev'
    },
    nextText: {
      type: String,
      default: 'next'
    },
    arrow: {
      type: String,
      default: 'hover'
    }
  },

  data() {
    return {
      list: [], // 当前显示的图片列表
      hover: false,
      timer: null,
      itemWidth: '',
      isReverse: false
    }
  },

  beforeMount() {
    this.itemWidth = 100 / this.total + '%'
    this.list = this.items.slice(0, this.total)
  },

  mounted() {
    if (this.autoplay) {
      this.startTimer()
    }
  },

  methods: {
    // 下一张
    next() {
      // 如果图片列表小于需要显示的数量，则不进行滚动
      if (this.items.length < this.total) {
        return
      }

      // 向后追加一个元素，该元素为：
      //    显示列表中最后一个元素在原数组中的后一个元素
      //    如果已经是最后一个元素，则使用第一个元素

      let indexOfItems = this.items.findIndex(
        item => item.id === this.list[this.list.length - 1].id
      )

      if (indexOfItems === this.items.length - 1) {
        // 使用第一个元素
        this.list.push(this.items[0])
      } else {
        // 使用后一个元素
        this.list.push(this.items[indexOfItems + 1])
      }
      // 移除当前显示图片中的第一个
      this.list.shift()
      this.isReverse = false
    },

    // 上一张
    prev() {
      // 如果图片列表小于需要显示的数量，则不进行滚动
      if (this.items.length < this.total) {
        return
      }
      // 向前追加一个元素, 该元素为：
      //    当前展示列表中的第一个元素在原数组中的前一个元素
      //    如果已经是第一个元素，则使用最后一个元素
      let indexOfItems = this.items.findIndex(
        item => item.id === this.list[0].id
      )

      if (indexOfItems === 0) {
        this.list.unshift(this.items[this.items.length - 1])
      } else {
        this.list.unshift(this.items[indexOfItems - 1])
      }
      // 移除当前显示列表中的最后一个元素
      this.list.pop()
      this.isReverse = true
    },

    // 点击图片
    selectedItem(item, index) {
      this.$emit('selectedItem', item, index)
    },

    // 开始计时器
    startTimer() {
      if (!this.interval || this.interval <= 0) {
        return
      }
      this.timer = setInterval(this.next, this.interval)
    },

    // 暂停计时器
    pauseTimer() {
      clearInterval(this.timer)
    },

    handleMouseEnter() {
      this.hover = true
      this.pauseTimer()
    },

    handleMouseLeave() {
      this.hover = false
      if (this.autoplay) {
        this.startTimer()
      }
    },

    // 列表过渡 beging
    beforeEnter(el) {
      el.style.opacity = 0
      if (this.isReverse) {
        el.style.transform = 'translateX(-100%)'
      } else {
        el.style.transform = 'translateX(100%)'
      }
    },

    enter(el, done) {
      Velocity(el, { opacity: 1, translateX: '0px' }, { complate: done })
    },

    beforeLeave(el) {
      el.style.position = 'absolute'
      if (this.isReverse) {
        el.style.right = 0
      } else {
        el.style.left = 0
      }
    },

    leave(el, done) {
      el.style.opacity = 0
      if (this.isReverse) {
        el.style.right = `-${this.itemWidth}`
        // el.style.transform = 'translateX(100%)'
      } else {
        el.style.transform = 'translateX(-100%)'
      }
      setTimeout(done, 1000)
    }
    // 列表过渡 end
  }
}
</script>

<style lang="less" scope>
.va-carousel {
  margin: 0 auto;
  overflow: hidden;
}

.image-list {
  width: 90%;
  height: 100%;
  position: relative;
  display: flex;
  flex-direction: row;
  align-items: center;
  box-sizing: border-box;
  margin: 0 auto;
}

.image-item {
  display: flex;
  flex-direction: row;
  align-items: center;
  padding: 0 20px;
  box-sizing: border-box;
  width: 100%;
  height: 100%;
  border-radius: 8px;
  cursor: pointer;
  transition: all 1s;

  &.active {
    transform: scale(1.2);
  }
  img {
    border-radius: 8px;
  }
}

.preview,
.next {
  position: absolute;
  font-size: 16px;
  color: #409eff;
  cursor: pointer;
}

.preview {
  left: 0;
  transform: translateX(-100%);
}
.next {
  right: 0;
  transform: translateX(100%);
}
</style>
