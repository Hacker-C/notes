# Vue-router路由

## 1 Vue路由简介和基础使用

### 1.1 什么是路由

- 路由器：设备和ip的映射关系
- nodejs路由：接口和服务的映射关系
- 前端路由：路径和组件的映射关系

### 1.2 为什么使用路由

> 目标: 在一个页面里, 切换业务场景

具体使用示例: 网易云音乐 https://music.163.com/

单页面应用(SPA): 所有功能在一个html页面上实现

前端路由作用: 实现业务场景切换

优点：

* 整体不刷新页面，用户体验更好

* 数据传递容易, 开发效率高

缺点：

* 开发成本高(需要学习专门知识)

* 首次加载会比较慢一点。不利于seo

### 1.3 vue-router介绍

> 目标: 如何在Vue项目中集成路由

官网: https://router.vuejs.org/zh/

vue-router模块包

它和 Vue.js 深度集成

可以定义 - 视图表(映射规则)

模块化的

提供2个内置全局组件

声明式导航自动激活的 CSS class 的链接

……

### 1.4 组件分类

> 目标:  .vue文件分2类, 一个是页面组件, 一个是复用组件

.vue文件本质无区别, 方便大家学习和理解, 总结的一个经验

src/views(或pages) 文件夹 和 src/components文件夹

* 页面组件 - 页面展示 - 配合路由用
* 复用组件 - 展示数据/常用于复用

> 总结: views下的页面组件, 配合路由切换, components下的一般引入到views下的vue中复用展示数据

### 1.5 vue-router使用

> 目标: 学会vue官方提供的vue-router路由系统功能模块使用

[vue-router文档](https://router.vuejs.org/zh/)

- 安装

```bash
yarn add vue-router
```

+ 导入路由

```js
import VueRouter from 'vue-router'
```

+ 使用路由插件

```jsx
// 在vue中，使用使用vue的插件，都需要调用Vue.use()
Vue.use(VueRouter)
```

+ 创建路由规则数组

```js
const routes = [
  {
    path: "/find",
    component: Find
  },
  {
    path: "/my",
    component: My
  },
  {
    path: "/part",
    component: Part
  }
]
```

+ 创建路由对象 -  传入规则

```jsx
const router = new VueRouter({
  routes
})
```

+ 关联到vue实例

```jsx
new Vue({
  router
})
```

+ components换成router-view

```vue
<router-view></router-view>
```

> 总结: 下载路由模块, 编写对应规则注入到vue实例上, 使用router-view挂载点显示切换的路由
>
> 总结: 一切都围绕着hash值变化为准

## 2 声明式导航

### 2.1 基础使用

> 目标: 可用全局组件router-link来替代a标签

1.  vue-router提供了一个全局组件 router-link
2.  router-link实质上最终会渲染成a链接 to属性等价于提供 href属性(to无需#)
3.  router-link提供了声明式导航高亮的功能(自带类名)

> 总结: 链接导航, 用router-link配合to, 实现点击切换路由

### 2.2 跳转传参

> 目标: 在跳转路由时, 可以给路由对应的组件内传值

在router-link上的to属性传值, 语法格式如下

* /path?参数名=值

* /path/值 – 需要路由对象提前配置 path: “/path/参数名”

对应页面组件接收传递过来的值

* $route.query.参数名

* $route.params.参数名

1. 创建components/Part.vue - 准备接收路由上传递的参数和值

   ```vue
   <template>
     <div>
         <p>关注明星</p>
         <p>发现精彩</p>
         <p>寻找伙伴</p>
         <p>加入我们</p>
         <p>人名: {{ $route.query.name }} -- {{ $route.params.username }}</p>
     </div>
   </template>
   ```

2. 路由定义

   ```js
   {
       path: "/part",
       component: Part
     },
     {
       path: "/part/:username", // 有:的路径代表要接收具体的值
       component: Part
     },
   ```

3. 导航跳转, 传值给MyGoods.vue组件

   ```vue
   <router-link to="/part?name=小传">朋友-小传</router-link>
   <router-link to="/part/小智">朋友-小智</router-link>
   ```

> 总结: 
>
> ?key=value   用$route.query.key 取值
>
> /值   提前在路由规则/path/:key  用$route.params.key  取值

## 3 重定向和模式

### 3.1 重定向

> 目标: 匹配path后, 强制切换到目标path上

* 网页打开url默认hash值是/路径
* redirect是设置要重定向到哪个路由路径

例如: 网页默认打开, 匹配路由"/", 强制切换到"/find"上

```js
const routes = [
  {
    path: "/", // 默认hash值路径
    redirect: "/find" // 重定向到/find
    // 浏览器url中#后的路径被改变成/find-重新匹配数组规则
  }
]
```

> 总结: 强制重定向后, 还会重新来数组里匹配一次规则

### 3.2 404页面

> 目标: 如果路由hash值, 没有和数组里规则匹配

默认给一个404页面

语法: 路由最后, path匹配*(任意路径) – 前面不匹配就命中最后这个, 显示对应组件页面

1. 创建NotFound页面

2. 在main.js - 修改路由配置

   ```js
   import NotFound from '@/views/NotFound'
   
   const routes = [
     // ...省略了其他配置
     // 404在最后(规则是从前往后逐个比较path)
     {
       path: "*",
       component: NotFound
     }
   ]
   ```

> 总结: 如果路由未命中任何规则, 给出一个兜底的404页面

### 3.2 路由 - 模式设置

> 目标: 修改路由在地址栏的模式

hash路由例如:  http://localhost:8080/#/home

history路由例如: http://localhost:8080/home  (以后上线需要服务器端支持, 否则找的是文件夹)

[模式文档](https://router.vuejs.org/zh/api/#mode)

在main.js中设置

```js
const router = new VueRouter({
  routes,
  mode: "history" // 打包上线后需要后台支持, 模式是hash
})
```

## 4 编程式导航

### 4.1 基础使用

> 目标: 用JS代码来进行跳转

语法:

```js
this.$router.push({
    path: "路由路径", // 都去 router/index.js定义
    name: "路由名"
})
```

1. main.js - 路由数组里, 给路由起名字

```json
{
    path: "/find",
    name: "Find",
    component: Find
},
{
    path: "/my",
    name: "My",
    component: My
},
{
    path: "/part",
    name: "Part",
    component: Part
},
```

2. App.vue - 换成span 配合js的编程式导航跳转

```vue
<template>
  <div>
    <div class="footer_wrap">
      <span @click="btn('/find', 'Find')">发现音乐</span>
      <span @click="btn('/my', 'My')">我的音乐</span>
      <span @click="btn('/part', 'Part')">朋友</span>
    </div>
    <div class="top">
      <router-view></router-view>
    </div>
  </div>
</template>

<script>
// 目标: 编程式导航 - js方式跳转路由
// 语法:
// this.$router.push({path: "路由路径"})
// this.$router.push({name: "路由名"})
// 注意:
// 虽然用name跳转, 但是url的hash值还是切换path路径值
// 场景:
// 方便修改: name路由名(在页面上看不见随便定义)
// path可以在url的hash值看到(尽量符合组内规范)
export default {
  methods: {
    btn(targetPath, targetName){
      // 方式1: path跳转
      this.$router.push({
        // path: targetPath,
        name: targetName
      })
    }
  }
};
</script>
```

### 4.2 跳转传参

> 目标: JS跳转路由, 传参

语法 query / params 任选 一个

```js
this.$router.push({
    path: "路由路径"
    name: "路由名",
    query: {
    	"参数名": 值
    }
    params: {
		"参数名": 值
    }
})

// 对应路由接收   $route.params.参数名   取值
// 对应路由接收   $route.query.参数名    取值
```

==格外注意: 使用path会自动忽略params==

App.vue

```vue
<template>
  <div>
    <div class="footer_wrap">
      <span @click="btn('/find', 'Find')">发现音乐</span>
      <span @click="btn('/my', 'My')">我的音乐</span>
      <span @click="oneBtn">朋友-小传</span>
      <span @click="twoBtn">朋友-小智</span>
    </div>
    <div class="top">
      <router-view></router-view>
    </div>
  </div>
</template>
<script>
export default {
  methods: {
    btn(targetPath, targetNmae) {
      // 方式1：用path跳转
      this.$router.push({
        // path: targetPath,
        name: targetNmae,
      });
      //
    },
  },
};
</script>
```

> 总结: 传参2种方式
>
> query方式 
>
> params方式 

##  5 嵌套和守卫

### 5.1 路由嵌套

> 目标: 在现有的一级路由下, 再嵌套二级路由

[二级路由示例-网易云音乐-发现音乐下](https://music.163.com/)

router-view嵌套架构图

1. 创建需要用的所有组件

   src/views/Find.vue -- 发现音乐页

   src/views/My.vue -- 我的音乐页

   src/views/Second/Recommend.vue  -- 发现音乐页 / 推荐页面

   src/views/Second/Ranking.vue      -- 发现音乐页 / 排行榜页面

   src/views/Second/SongList.vue     -- 发现音乐页 / 歌单页面

2. main.js– 继续配置2级路由

   一级路由path从/开始定义

   二级路由往后path直接写名字, 无需/开头

   嵌套路由在上级路由的children数组里编写路由信息对象

3. 说明：

   App.vue的router-view负责发现音乐和我的音乐页面, 切换

   Find.vue的的router-view负责发现音乐下的, 三个页面, 切换

   1. 在Find.vue中

```vue
<template>
  <div>
    <!-- <p>推荐</p>
    <p>排行榜</p>
    <p>歌单</p> -->
    <div class="nav_main">
      <router-link to="/find/recommend">推荐</router-link>
      <router-link to="/find/ranking">排行榜</router-link>
      <router-link to="/find/songlist">歌单</router-link>
    </div>

    <div style="1px solid red;">
      <router-view></router-view>
    </div>
  </div>
</template>
<script>
export default {};
</script>
<style scoped>
</style>
```

2. 配置路由规则-二级路由展示

```js
const routes = [
  // ...省略其他
  {
    path: "/find",
    name: "Find",
    component: Find,
    children: [
      {
        path: "recommend",
        component: Recommend
      },
      {
        path: "ranking",
        component: Ranking
      },
      {
        path: "songlist",
        component: SongList
      }
    ]
  }
  // ...省略其他
]
```

3. 说明：

* App.vue, 外层的router-view负责发现音乐和我的音乐页面切换

* Find.vue 内层的router-view负责发现音乐下的子tab对应的组件切换

4. 运行 - 点击导航观察嵌套路由在哪里展示

> 总结: 嵌套路由, 找准在哪个页面里写router-view和对应规则里写children

### 5.2 声明导航 - 类名区别

> 目标: router-link自带的2个类名的区别是什么

观察路由嵌套导航的样式

* router-link-exact-active  (精确匹配) url中hash值路径, 与href属性值完全相同, 设置此类名

* router-link-active             (模糊匹配) url中hash值,    包含href属性值这个路径

### 5.3 全局前置守卫

> 目标: 路由跳转之前, 先执行一次前置守卫函数, 判断是否可以正常跳转

使用例子: 在跳转路由前, 判断用户登陆了才能去<我的音乐>页面, 未登录弹窗提示回到发现音乐页面

1. 在路由对象上使用固定方法beforeEach

```js
// 目标: 路由守卫
// 场景: 当你要对路由权限判断时
// 语法: router.beforeEach((to, from, next)=>{//路由跳转"之前"先执行这里, 决定是否跳转})
// 参数1: 要跳转到的路由 (路由对象信息)    目标
// 参数2: 从哪里跳转的路由 (路由对象信息)  来源
// 参数3: 函数体 - next()才会让路由正常的跳转切换, next(false)在原地停留, next("强制修改到另一个路由路径上")
// 注意: 如果不调用next, 页面留在原地

// 例子: 判断用户是否登录, 是否决定去"我的音乐"/my
const isLogin = true; // 登录状态(未登录)
router.beforeEach((to, from, next) => {
  if (to.path === "/my" && isLogin === false) {
    alert("请登录")
    next(false) // 阻止路由跳转
  } else {
    next() // 正常放行
  }
})
```

> 总结: next()放行, next(false)留在原地不跳转路由, next(path路径)强制换成对应path路径跳转