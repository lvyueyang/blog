---
title: vue 使用 contenteditable 模拟 input 输入框  
tag: HTML,Vue,小示例  
---  

``` html
<template>
    <div class="div-input"
         ref="divInputRef"
         :class="value.length > 0 ? 'none-placeholder' : ''"
         :style="{'min-width': minWidth}"
         :contenteditable="input"
         :placeholder="placeholder"
         @focus="ischecked = true"
         @blur="blurFn"
         @input="inputFn"
         v-html="text"></div>
</template>
```

``` js
export default {
    name: 'DivInput',
    props: {
        input: {
            type: Boolean,
            default: true
        },
        minWidth: {
            type: String,
            default: '4em'
        },
        placeholder: {
            type: String,
            default: ''
        },
        value: {
            type: String,
            default: ''
        }
    },
    data() {
        return {
            ischecked: false,
            text: this.value
        }
    },
    mounted() {},
    watch: {
        value(val) {
            // 解决光标跳动BUG
            if (!this.ischecked) {
                this.text = val || ' '
            }
            if (!val) {
                this.text = ''
                this.$refs.divInputRef.innerHTML = ''
            }
        }
    },
    methods: {
        inputFn(e) {
            const val = e.target.innerHTML
            this.$emit('input', val)
        },
        blurFn(e) {
            this.ischecked = false
            this.text = this.value
            e.view.blur()
        }
    }
}

```
```scss
.div-input {
    position: relative;
    display: inline-block;
    padding: 0 5px;
    cursor: text;
    outline: none;
    &:before {
        position: absolute;
        top: 0;
        left: 0;
        content: attr(placeholder);
        color: #999;
    }
    &.none-placeholder {
        &:before {
            display: none;
        }
    }
}
```  
  