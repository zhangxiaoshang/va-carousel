<template>
  <div id="app">
    <h1>一个基于vue的图片轮播组件</h1>

    <p>该组件实现上参考ElementUI/carousel组件</p>

    <h3>Demo1 默认效果</h3>
    <ol>
      <li>间隔2s自动切换一次</li>
      <li>鼠标悬停时显示切换按钮,并停止自动切换</li>
      <li>显示列表中的图片为奇数时，突出显示中间图片</li>
    </ol>
    <VaCarousel/>

    <h3>Demo2 为组件设置一些属性</h3>
    <ol>
      <li>自动切换的间隔设为1s</li>
      <li>始终显示切换按钮并自定义了显示的文字，也可以通过solt使用你喜欢的iconfont</li>
      <li>点击图片时触发点击事件</li>
      <li>可以
        <a href="https://github.com/zhangxiaoshang/va-carousel#readme"> 点击这里 </a>查看所有支持的属性、事件、solt</li>
    </ol>
    <VaCarousel total="8"
      interval=1000
      prevText="上一张"
      nextText="下一张"
      arrow="always"
      @selectedItem="selectedItem"></VaCarousel>

  </div>
</template>

<script>
import VaCarousel from './components/VaCarousel'

export default {
  name: 'App',
  components: {
    VaCarousel
  },
  methods: {
    selectedItem(item, index) {
      alert(`点击了第${index}张图片`)
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: left;
  color: #2c3e50;
  margin-top: 60px;
}

h1 {
  text-align: center;
}
</style>
