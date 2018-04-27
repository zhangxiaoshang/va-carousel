# va-carousel

> A Vue.js project

## Build Setup

```bash
# install dependencies
npm install

# serve with hot reload at localhost:8080
npm run dev

# build for production with minification
npm run build

# build for production and view the bundle analyzer report
npm run build --report

# run unit tests
npm run unit

# run e2e tests
npm run e2e

# run all tests
npm test
```

For a detailed explanation on how things work, check out the [guide](http://vuejs-templates.github.io/webpack/) and [docs for vue-loader](http://vuejs.github.io/vue-loader).

### Attributes

| 参数      | 说明                                                  | 类型    | 可选值             | 默认值 |
| --------- | ----------------------------------------------------- | ------- | ------------------ | ------ |
| items     | 数据列表                                              | array   | -                  | -      |
| total     | 需要显示的图片数量,当数量为奇数时，中间图片会  被放大 | number  | -                  | 7      |
| height    | 走马灯的高度                                          | string  | -                  | 180px  |
| width     | 走马灯的宽度                                          | string  | -                  | 90%    |
| imgWidth  | 图片宽度                                              | string  | -                  | 100%   |
| imgHeight | 图片高度                                              | string  | -                  | 70%    |
| autoplay  | 是否自动切换                                          | boolean | -                  | true   |
| interval  | 自动切换的时间间隔，单位为毫秒                        | number  | -                  | 2000   |
| prevText  |  向上箭头上显示的内容                                 | string  | -                  | prev   |
| nextText  | 向下箭头上显示的内容                                  | string  | -                  | next   |
| arrow     | 切换  按钮的显示时机                                  | string  | always/hover/never | hover  |

### Events

| 事件名称     | 说明           | 回调参数                             |
| ------------ | -------------- | ------------------------------------ |
| selectedItem | 点击图片时触发 | 当前图片对象，当前图片在列表中的位置 |

### Slot

| name | 说明                 |
| ---- | -------------------- |
| prev | 向上  箭头区域的内容 |
| next | 向下箭头区域的内容   |
