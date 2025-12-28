# Vue3 实战后台管理

基于 B 站 https://www.bilibili.com/video/BV1LS421d7cY

## 项目初始化

~~~shell
# 使用 vite 创建项目
yarn create vite
~~~

### 添加别名

修改 vite.config.js：

~~~javascript
import {defineConfig} from 'vite'
import vue from '@vitejs/plugin-vue'

// https://vite.dev/config/
export default defineConfig({
    plugins: [vue()],

    // 添加别名，后面路径可以使用 @ 来代替 /src 路径
    resolve: {
        alias: [
            {
                find: "@",
                replacement: "/src"
            }
        ]
    }
})
~~~

### 添加路由

~~~shell
yarn add vue-router@4
~~~

在 src 下创建 router/index.js。

~~~javascript
import {createRouter, createWebHistory} from "vue-router";

const router = createRouter({
    history: createWebHistory(),
    routes: [
        {path: "/", name: 'main', component: () => import('@/views/Main.vue')},
    ]
})

export default router
~~~

注册路由，修改 src/main.js

~~~javascript
import { createApp } from 'vue'
import './style.css'
import App from './App.vue'
import router from "./router/index.js";

const app = createApp(App)
app.use(router)
app.mount('#app')
~~~

### 通用 CSS

在 src 下创建 sytles/reset.css

~~~css
/* reset.css */
*,
*::before,
*::after {
    box-sizing: border-box;
}

html, body, #app {
    margin: 0;
    padding: 0;
    width: 100%;
    height: 100%;
}

/* 可选：让弹性图片/视频更乖 */
img, svg, video, canvas {
    max-width: 100%;
    display: block;
}

/* 可选：去掉列表默认 indent */
ul, ol {
    margin: 0;
    padding: 0;
    list-style: none;
}

/* 可选：按钮、输入框字体继承，防止浏览器默认字体大小 */
button, input, optgroup, select, textarea {
    font-family: inherit;
    font-size: 100%;
}
~~~

在 main.js 引入：

~~~javascript
import '@/styles/reset.css'
~~~

### 创建 Main.vue

在 views 下创建 Main.vue：

~~~vue
<script setup>

</script>

<template>
  <div>我是 Main 组件</div>
</template>

<style scoped>

</style>
~~~

### 配置 App.vue

~~~vue
<script setup>
</script>

<template>
  <router-view></router-view>
</template>

<style scoped>

</style>
~~~

### 启动项目

~~~shell
# 启动
yarn run dev

# 访问
http://localhost:5173/

# 可以看到展示的是 我是 Main 组件
~~~

## 安装 element-plus

[快速开始 | Element Plus](https://element-plus.org/zh-CN/guide/quickstart)

### 按需导入

~~~shell
# 安装依赖
yarn add element-plus
yarn add -D unplugin-vue-components unplugin-auto-import
~~~

配置 vite.config.ts：

~~~javascript
import {defineConfig} from 'vite'
import vue from '@vitejs/plugin-vue'

// 新增
import AutoImport from 'unplugin-auto-import/vite'
import Components from 'unplugin-vue-components/vite'
import {ElementPlusResolver} from 'unplugin-vue-components/resolvers'

export default defineConfig({
    plugins: [
        vue(),
        // 新增
        AutoImport({
            resolvers: [ElementPlusResolver()],
        }),
        Components({
            resolvers: [ElementPlusResolver()],
        }),],

    resolve: {
        alias: [
            {
                find: "@",
                replacement: "/src"
            }
        ]
    }
})
~~~

### 添加图标

[Icon 图标 | Element Plus](https://element-plus.org/zh-CN/component/icon)

~~~shell
yarn add @element-plus/icons-vue
~~~

修改 main.js，全部导入

~~~javascript
import { createApp } from 'vue'
import './style.css'
import App from './App.vue'
import router from "./router/index.js";
// 全局导入图标
import * as ElementPlusIconsVue from '@element-plus/icons-vue'


const app = createApp(App)
app.use(router)
// 注册图标
for (const [key, component] of Object.entries(ElementPlusIconsVue)) {
    app.component(key, component)
}

app.mount('#app')
~~~

直接引入即可

~~~html
<el-icon><InfoFilled /></el-icon>
~~~

