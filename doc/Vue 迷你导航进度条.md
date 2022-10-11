---
title: Vue 迷你导航进度条  
tag: JavaScript,Vue,小示例  
---  

``` html
<template>
    <div class="scroll-mini" ref="s">
        <span class="block" :style="`left:calc(${range})`" ref="p"></span>
    </div>
</template>

<script>
    export default {
        name: "ScrollMini",
        props: {
            refName: String
        },
        data() {
            return {
                range: 0,
                width: 0
            }
        },
        mounted() {
            this.$nextTick(() => {
                const dom = this.$parent.$refs[this.refName]
                const s = this.$refs['s'].offsetWidth
                const p = this.$refs['p'].offsetWidth
                dom.addEventListener('scroll', e => {
                    const target = e.target
                    const {scrollLeft, scrollWidth, offsetWidth} = target
                    let l = scrollLeft / (scrollWidth - offsetWidth)
                    this.range = l * (s - p) + 'px'
                })
            })
        },
        methods: {}
    }
</script>

<style lang="scss" scoped>
    .scroll-mini {
        width: 100px;
        height: 15px;
        margin: 0 auto;
        border-radius: 10px;
        background: #eee;

        .block {
            position: relative;
            height: 15px;
            width: 40px;
            display: block;
            background: rgb(25, 137, 250);
            border-radius: 10px;
        }
    }
</style>
```  
  