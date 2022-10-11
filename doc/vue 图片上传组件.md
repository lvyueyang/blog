---
title: vue 图片上传组件  
tag: 图片处理,Vue,ES6,文件上传  
---  

## 页面
> 使用了iview中的icon组件，不需要请自行替换
``` html
<template>
    <div class="file-img" :class="{loading}">
        <Icon class="icon" type="ios-add"/>
        <img v-show="value" :src="value" alt="">
        <input type="file" @change="handleChange">
    </div>
</template>

<script>
    export default {
        name: "FILE-IMG",
        props: {
            value: String
        },
        data() {
            return {
                loading: false
            }
        },
        components: {},
        created() {
        },
        methods: {
            handleChange(e) {
                console.log(e.target.files[0])
            },
            async uploadFile(file) {
                let formData = new FormData()
                formData.append('file', file)
                this.loading = true
                try {
                    let res = await this.$http('/file', formData)
                    this.$emit('input', res.data.url)
                } catch (e) {
                    this.$emit('input', '')
                    alert('文件上传失败')
                }
                this.loading = false
            }
        },
    }
</script>

<style lang="scss">
    .file-img {
        position: relative;
        width: 135px;
        height: 135px;
        border: 1px dashed #ccc;
        display: inline-block;
        font-size: 135px;
        color: #ccc;
        input {
            position: absolute;
            opacity: 0;
            left: 0;
            top: 0;
            width: 100%;
            height: 100%;
            z-index: 10;
        }
        img {
            position: absolute;
            left: 0;
            top: 0;
            display: block;
            width: 100%;
            height: 100%;
            z-index: 2;
        }
        &.loading {
            &:after {
                content: '上传中...';
                color: #fff;
                line-height: 135px;
                text-align: center;
                font-size: 16px;
                position: absolute;
                left: 0;
                top: 0;
                width: 100%;
                height: 100%;
                background: rgba(0, 0, 0, .7);
                z-index: 11;
            }
        }
    }
</style>
```  
  