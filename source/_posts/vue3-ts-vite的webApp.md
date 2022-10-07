---
title: vue3+ts+vite的webApp
date: 2022-10-07 22:17:14
tags: "vue3"
categories: 
- web前端
---
为了熟悉vue3+ts的开发风格，搭建的一个仿小红书的WebApp（已开源）;持续迭代中......
 <!-- more -->
### gitHub仓库 ：[https://github.com/xxljunjun/vue3-webApp](https://github.com/xxljunjun/vue3-webApp)
#### 线上地址：[http://www.xxljunjun.com/redbook](http://www.xxljunjun.com/redbook)
#### 一、搭建项目
+ npm init vite@latest
**踩坑：vite项目需要node版本大于16！！！**
+ 通过vite@latest创建的是vite3.0.7的版本
+ npm run dev启动项目
![](https://upload-images.jianshu.io/upload_images/26121995-9a20562fd35ff131.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### 二、配置路径别名
**踩坑：vite中不支持require()语法！！！**
+ 编辑vite.config.ts
```
//如果报错就安装：npm install --save-dev @types/node
import path from 'path'
import { defineConfig } from 'vite'

// https://vitejs.dev/config/
export default defineConfig({
    resolve:{
      // 配置路径别名
      alias: {
        '@': path.resolve(__dirname, './src'),
      },
    },
})
```
### 三、安装css预编译语言（sass、less、stylus三者选一即可）
```js
// # Sass
npm install -D sass-loader sass

// # Less
npm install -D less-loader less

// # Stylus
npm install -D stylus-loader stylus

npm install style-resources-loader -D
```

### 四、配置路由
+ 1、npm install -S vue-router@next
+ 2、新建路由文件：vue3-webApp/src/router/index.js
```
import { createRouter, createWebHashHistory } from "vue-router";

const routes = [
    {
        path: "/",
        name: "home",
        //记得顺便新建home文件的index.vue组件
        component: () => import("@/views/home/index.vue"),
    }
]

const router = createRouter({
    history: createWebHashHistory(),
    routes
});

export default router;
```
+3、更改App.vue文件
```vue
<template>
  <router-view></router-view>
</template>
```
+ 4、更改main.ts文件
```
import { createApp } from 'vue'
import App from './App.vue'
import router from '@/router/index.js'

//创建应用实例对象
const app = createApp(App)
app.use(router).mount('#app')
```
+ 5、路由在vue文件中的使用
```
<script setup lang="ts">
import { useRouter, useRoute } from "vue-router";
const router = useRouter();
const goBack = () => {
  router.push({ path: "/home" });
};
</script>
```
#### 五、安装vant-UI组件库
```js

npm install vant -S

//按需引入
npm i unplugin-vue-components -D
//需要配置vite.config

```
+vant支持vue3：[https://vant-contrib.gitee.io/vant/#/zh-CN](https://vant-contrib.gitee.io/vant/#/zh-CN) 
![vant官网](https://upload-images.jianshu.io/upload_images/26121995-0c8ff4ec22ff734d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

#### 六、移动端适配
+ npm install postcss-pxtorem --save-dev
+ npm install amfe-flexible --save-dev
+ 配置main.ts
```
import { createApp } from 'vue'
import App from './App.vue'
import router from './router'
// 移动端适配
import 'amfe-flexible'

//创建应用实例对象
const app = createApp(App)
app.use(router).mount('#app')
```
+ 配置vite.config.js
```js
//vite.config.js中配置postcss-pxtorem
export default defineConfig({
  css: {
    postcss: {
      plugins: [
        postCssPxToRem({
          rootValue: 37.5, // 1rem的大小
          propList: ['*'], // 需要转换的属性，这里选择全部都进行转换
        })
      ]
    }
  },
})
```
#### 七、vue3中的事件总线通信
**在vue3中兄弟组件之间的通信不存在eventBus了，官方推荐使用mitt**
```js
npm install --save mitt
//bus.js
import mitt from "mitt";
const emitter = mitt()
export default emitter
//使用
emitter.emit()
emitter.on()
```
#### 最后
这个vue3+ts+vite的前端Web项目就搭建完了，可以进行页面的开发了！！！
缺陷：暂时还没有加入vuex的通信，感兴趣的同学可以自己去探索一下









