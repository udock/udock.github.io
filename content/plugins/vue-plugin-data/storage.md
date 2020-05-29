# Vue data 扩展： storage

## 概述

data storage 扩展的功能很简单，就是将 LocalStorage 中的数据双向绑定到 vue data 属性上。实现将 data 上属性读写映射到 LocalStorage 上。

## 插件安装及配置

安装：

```bash
npm i @udock/vue-plugin-data--storage
```

配置： 在 src/udock.config.js 中添加配置

```js
module.exports = {
  ...
  [
    'data',
    {
      plugins: [
        'storage'
      ]
    }
  ]
  ...
}
```

## 使用语法

在 data 中的普通属性后添加 @storage，例如：

```js
export default {
  data () {
    return {
      'key1@storage': 'key1', // 将 this.key1 和 LocalStorage 中的 key1 属性绑定，并且只读
      'key2@storage': ['key2'], // 将 this.key2 和 LocalStorage 中的 key2 属性绑定，可读可写
      'key3@storage': ['key3', 'default'], // 将 this.key3 和 LocalStorage 中的 key3 属性绑定，可读可写，默认值为 default
      'key4@storage': { path: 'key4', readonly: true, default: 'default' } // 将 this.key4 和 LocalStorage 中的 key4 属性绑定，只读，默认值为 default
    }
  }
}
```

在模板中像使用普通属性一样使用即可。

## 使用示例

```js
<template>
<div>
  {{key1}}
  <ElInput v-model="key1"></ElInput>
</div>
</template>

<script>
export default {
  data () {
    return {
      'key1@storage': ['key1', 'default']
    }
  }
}
</script>
```

可以在文本框中修改值，然后刷新页面，可以看到刷新后值被保留下来了
