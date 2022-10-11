---
title: webstorm Vue 模板  
tag: Vue,IDE,webstorm  
---  

## 页面
``` html
<template>
    <div>#[[$END$]]#</div>
</template>

<script>
export default {
name: "${COMPONENT_NAME.toUpperCase()}",
data(){
    return{}
},
components:{},
created(){},
methods:{},
}
</script>

<style lang="scss">

</style>

```
## 组件
```html
<template>
    <div>#[[$END$]]#</div>
</template>

<script>
export default {
name: "${COMPONENT_NAME.toUpperCase()}",
props:{},
data(){
    return{}
},
watch:{},
components:{},
created(){},
methods:{},
}
</script>

<style lang="scss">

</style>

```  
  