<!--
注意：具有交互功能的说明文档，需要有<script></script>标签，在标签元素中定义需要导出的vue实例。
在:::demo ::: 代码块中定义的模版<template></template>会作为导出的vue实例的模版，但是在代码块中的<script></script>中的内容仅作为展示，需注意。

！！！组件和文档不必写在一起，:::demo ::: 代码块中的组件引入，可通过npm在main中全局引入插件库，然后调用；
      比如本输入框用到的组件jy-input，因为该组件已全局注册，故可以使用； 同理，由于本项目已引入elementUI，可把jy-input替换为el-input,同样生效！！！
      故组件库插件和说明文档项目可拆开。
-->
<script>
export default {
  data () {
    return {
      value: '测试测试'
    }
  }
}
</script>
## Input
介绍Input的使用
:::demo
``` html
<template>
  <jy-input
    :value="value"
  ></jy-input>
</template>
<script>
export default {
  data () {
    return {
      value: '测试测试'
    }
  }
}
</script>
```
:::
