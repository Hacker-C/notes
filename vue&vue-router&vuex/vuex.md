# Vuex状态管理

## 一、state:存储数据

### 1.定义state：

```js
state: {
  count: 0,
  price: 100
},
```

### 2.原始方式：通过{{$store.state.变量名}}

```vue
<p>组件A{{ $store.state.count }}</p>
```

### 3.辅助函数方式：mapState

#### 3.1 引入mapState

```js
import { mapState } from "vuex";
```

#### 3.2 在computed里，通过...mapState(['变量名1'])

```js
computed:{
    ...mapState(['count'])
}
```

#### 3.3 使用变量，通过{{变量名}}

```vue
<p>{{count}}</p>
```

## 二、mutations：同步修改数据

### 1.定义mutations 

```js
mutations: {
    setCount(state, val) {
        state.count += val.a
}
```

### 2.原始方式：methods里，通过this.$store.commit

```js
 methods: {
    btn() {
      this.$store.commit("setCount", { a: 1, b: 2 });
    }
}
```

### 3.辅助函数方式：mapMutations

#### 3.1 引入mapMutations

```js
import {mapMutations} from 'vuex'
```

#### 3.2 在methods里，通过....mapMutations(["方法名"])

```js
...mapMutations(["setCount"]),
```

#### 3.3 在标签中绑定事件

```vue
<button @click="setCount({ a: 1, b: 2 })">修改数据</button>
```

## 三、actions:异步操作数据

### 1.定义actions

```js
actions: {
    //一般为ajax请求
    setCount2(context, val) {
      setTimeout(() => {
        context.commit('setCount', val)
      }, 1000);
    }
},
```

### 2.原始方式：在methods里，通过 this.$store.$dispatch

```js
btn2() {
    this.$store.$dispatch("setCount2", { a: 1, b: 2 });
},
```

### 3.辅助函数方式：mapActions

#### 3.1 引入mapActions

```js
import {mapActions} from "vuex";
```

#### 3.2 在methods里，通过....mapActions(["方法名"])

```js
  methods: {
    ...mapActions(["setCount2"]),
  },
```

#### 3.3 在标签中绑定事件

```vue
<button @click="setCount2({ a: 1, b: 2 })">异步修改数据</button>
```

## 四、getters:处理数据

### 1.定义getters

```js
getters: {
    showCount(state) {
      if (state.count == 0) {
        return '男'
      } else if (state.count == 1) {
        return '女'
      } else {
        return '人妖'
      }
    }
},
```

### 2.原始方式：$store.getters.方法名

```vue
<P>{ $store.getters.showCount }}</P>
```

### 3.辅助函数方式:mapGetters

#### 3.1 引入mapGetters

```js
import { mapGetters } from "vuex";
```

#### 3.2 在computed里，通过 ...mapGetters(["方法名"])

```js
computed: {
  ...mapGetters(["showCount"]),
},
```

#### 3.3 在标签中绑定事件

```vue
<button @click="setCount2({ a: 1, b: 2 })">异步修改数据</button>
```

## 五、modules模块化

### 1. 模块化的简单应用

#### 1. 1. 定义modules

```js
const store  = new Vuex.Store({
  modules: {
    user: {
       state: {
         token: '12345'
       }
    },
    setting: {
      state: {
         name: 'Vuex实例'
      }
    }
  })
```

#### 1.2. 直接调用

```html
<template>
  <div>
      <div>用户token {{ $store.state.user.token }}</div>
      <div>网站名称 {{ $store.state.setting.name }}</div>
  </div>
</template>
```

#### 1.3. 通过getters修改

```js
const store  = new Vuex.Store({
     getters: {
   token: state => state.user.token,
   name: state => state.setting.name
	} 
}
```

#### 1.4. 通过mapGetters引用

```js
 computed: {
       ...mapGetters(['token', 'name'])
 }
```

### 2. 命名空间

#### 2.1. 定义

在store/index.js中，定义modules

```js
import Vue from 'vue'
import Vuex from 'vuex'
Vue.use(Vuex)

export default new Vuex.Store({
...
modules:{
       user: {
        //开启命名空间
      namespaced: true,
      state: {
        token: '12345'
      },
      mutations: {
        //  这里的state表示的是user的state
         updateToken (state) {
            state.token = 678910
         }
       }
    }, 
})
```

#### 2.2. 直接调用

```js
methods:{
    test(){
        this.$store.dispatch('user/updateToken')
    }
}
```

#### 2.3. 通过辅助函数调用

```js
methods:{
     ...mapMutations(['user/updateToken']),
       test () {
           this['user/updateToken']()
       }
}
```

#### 2.4. createNamespacedHelpers

```js
import {createNamespacedHelpers} from 'vuex'
const {mapMutations} =createNamespacedHelpers('user')
export default {
...
    methods:{
        ...mapMutations(['updateToken'])
    }
}
```
