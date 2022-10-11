---
title: vue中使用 contenteditable 制作输入框并使用v-model做双向绑定  
tag: HTML,Vue,ES6  
---  

```html
<template>
  <div class="div-input"
       :class="value.length > 0 ? 'placeholder_hide' : ''"
       :style="{'min-width': minWidth}"
       :contenteditable="input"
       :placeholder="placeholder"
       @focus="ischecked = true"
       @blur="blurFn"
       @input="inputFn"
       v-html="text"></div>
</template>

<script>
  export default {
    name: 'DivInput',
    props: {
      input: {
        type: Boolean,
        default: true
      },
      minWidth: {
        type: String,
        default: '2.2em'
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
    data () {
      return {
        ischecked: false,
        text: this.value
      }
    },
    mounted () {
    },
    watch: {
      value () {
        // 解决光标跳动BUG
        if (!this.ischecked) {
          this.text = this.value
        }
      }
    },
    methods: {
      inputFn (e) {
        const val = e.target.innerHTML
        this.$emit('input', val)
      },
      blurFn (e) {
        this.ischecked = false
        this.text = this.value
        e.view.blur()
      }
    }
  }
</script>

<style lang="scss">
  .div-input {
    display: inline-block;
    min-width: 4em;
    border-bottom: 1px solid #ccc;
    outline: none;
    padding: 0 5px;
    &:focus{
      border-color: #333;
    }
    &:before {
      content: attr(placeholder);
      white-space: nowrap;
      width: 100%;
      color: #aaa;
      z-index: 0;
      cursor: text;
    }
    &.placeholder_hide {
      &:before {
        display: none;
      }
    }
  }
</style>
```  
  