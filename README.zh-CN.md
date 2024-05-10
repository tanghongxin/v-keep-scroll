# v-keep-scroll

[English README](README.en-US.md)

v-keep-scroll 可以在 activated 和 deactivated 之间保持 keep-alive 组件下的元素的滚动位置。

## 安装

```bash
pnpm add v-keep-scroll
```

### 全局引入

```javascript
import { createApp } from "vue";
import plugin from "v-keep-scroll";
import App from "./App.vue";

const app = createApp(App);
app.use(plugin)
app.mount("#app");
```

（可选）如果您使用 TypeScript，请在 jsconfig.json 或 tsconfig.json 中添加类型声明以获得类型提示。

```json
{
  "compilerOptions": {
    "types": [
      "v-keep-scroll/types"
    ]
  }
}
```

### 手动引入

```javascript
import { KeepScroll, vKeepScroll } from "v-keep-scroll";

export default {
  components: { KeepScroll },
  directives: { keepScroll: vKeepScroll },
}
```

## 使用方法

无论是针对指令还是组件，它们都应该作用于特定的单个元素，而不是 template 或 teleport 等虚拟元素，并且它们必须设置一个特定的高度并且可滚动。

```css
.scrollable {
  /* 高度应为具体值或有效的百分比 */
  height: 100px; 
  overflow: auto;
}
```

```html
<!-- 应用于当前元素 -->
<div class="scrollable" v-keep-scroll>
  <div id="child"></div>
</div>

<!-- 应用于单个子元素，通过字符串选择器 -->
<div v-keep-scroll="#child">
  <div class="scrollable" id="child"></div>
</div>

<!-- 应用于多个子元素，通过字符串选择器数组 -->
<div v-keep-scroll="['#child', '.content']">
  <div class="scrollable" id="child"></div>
  <div class="scrollable" id="content"></div>
</div>

<!-- 通过包装元素应用指令，标签默认为 "div" -->
<keep-scroll tag="div" class="scrollable">
  <div id="child"></div>
</keep-scroll>
```