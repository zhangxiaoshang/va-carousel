# va-carousel

> 一个基于 vue 的图片轮播组件

## 体验

方式 1

在线Demo  [http://va-carousel.xiaoshang.online](http://va-carousel.xiaoshang.online)

方式 2

```bash
git clone https://github.com/zhangxiaoshang/va-carousel.git
cd va-carousel
npm install
npm start
```

## 使用

1.使用 vue-cli 构建一个项目

```bash
# 这里默认你已经安装了vue-cli
vue init webpack vue-project
```

2.安装 va-carousel

```bash
cd vue-project
npm install --save va-carousel
```

3.导入组件

在需要使用 VaCarousel 的组件中，导入组件

js 部分

```js
<script>
import VaCarousel from 'va-carousel/src/components/VaCarousel'

export default {
  name: 'App',
  components: {
    VaCarousel
  }
}
</script>
```

template 部分

```html
<template>
  <div id="app">
    <VaCarousel/>
  </div>
</template>
```

4.启动项目

```bash
npm run dev
```

### Attributes

| 参数      | 说明                                                                           | 类型    | 可选值             | 默认值 |
| --------- | ------------------------------------------------------------------------------ | ------- | ------------------ | ------ |
| items     | 数据列表, 每个元素是一个对象，其中 id、src 属性是必需要有的(不允许有重复的 id) | array   | -                  | -      |
| total     | 需要显示的图片数量,当数量为奇数时，中间图片会
被放大                          | number  | -                  | 7      |
| height    | 走马灯的高度                                                                   | string  | -                  | 180px  |
| width     | 走马灯的宽度                                                                   | string  | -                  | 90%    |
| imgWidth  | 图片宽度                                                                       | string  | -                  | 100%   |
| imgHeight | 图片高度                                                                       | string  | -                  | 70%    |
| autoplay  | 是否自动切换                                                                   | boolean | -                  | true   |
| interval  | 自动切换的时间间隔，单位为毫秒                                                 | number  | -                  | 2000   |
| prevText  | 向上箭头上显示的内容                                                           | string  | -                  | prev   |
| nextText  | 向下箭头上显示的内容                                                           | string  | -                  | next   |
| arrow     | 切换箭头的显示时机                                                             | string  | always/hover/never | hover  |

### Events

| 事件名称     | 说明           | 回调参数                             |
| ------------ | -------------- | ------------------------------------ |
| selectedItem | 点击图片时触发 | 当前图片对象，当前图片在列表中的位置 |

### Slot

| name | 说明               |
| ---- | ------------------ |
| prev | 向上箭头区域的内容 |
| next | 向下箭头区域的内容 |
