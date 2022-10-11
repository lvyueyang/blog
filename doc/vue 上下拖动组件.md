---
title: vue 上下拖动组件  
tag: Vue,ES6,小示例  
---  

```html

<template>
    <div class="fixed"
          :style="{transform : `translateY(${range}px)`}"
          @touchstart="handlerStart"
          @touchend="handlerEnd"
          @touchmove="handlerMove">
    </div>
</template>

<script>
    const bodyScroll = function (event) {
        event.preventDefault()
    }
    export default {
        name: "FIXED-LOGO",
        props: {},
        data() {
            return {
                startInit: 0,
                range: 0,
                once: true,
                endPost: 0
            }
        },
        created() {
        },
        methods: {
            handlerStart(e) {
                this.startInit = parseInt(e.touches[0].clientY)
                if (this.range !== 0) {
                    this.once = false
                }
                if (!this.once) {
                    this.endPost = this.range
                }
                document.body.addEventListener('touchmove', bodyScroll, {passive: false})
            },
            handlerMove(e) {
                const Y = parseInt(e.touches[0].clientY)
                const range = Y - this.startInit
                if (this.once) {
                    this.range = range
                } else {
                    this.range = this.endPost + range
                }
            },
            handlerEnd() {
                this.startInit = 0
                document.body.removeEventListener('touchmove', bodyScroll, {passive: false})
            }
        },
    }
</script>
```  
  