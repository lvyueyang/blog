---
title: Vue 多图上传组件  
tag: Vue,小示例,组件  
---  

```html
<template>
    <div class="upload-img-list-wrapper">
        <div class="item add-file" title="点击上传">
            <div class="file-input">
                <input type="file"
                       multiple
                       accept="image/gif,image/jpeg,image/jpg,image/png,image/svg"
                       @change="handlerFile"
                >
            </div>
        </div>
        <div class="item" v-for="(v,index) in fileList">
            <div class="img"><img :src="v.url" alt=""></div>
            <div class="loading" v-if="v.loading"></div>
            <span class="close" title="删除" @click="removeItem(index)">❎</span>
            <span class="upload" title="重新上传" @click="againUploadFile(v)">⬆️</span>
            <div class="operate">
                <div title="向左移动" @click="zIndexDown(index)">👈</div>
                <div title="放大" @mouseout="v.bigShow = false" @mouseover="v.bigShow = true">🔍</div>
                <div title="向右移动" @click="zIndexUp(index)">👉</div>
            </div>
            <div class="big-wrapper-img" v-show="v.bigShow">
                <img :src="v.url" alt="">
            </div>
        </div>
    </div>
</template>

<script>
    import fileUpload from '../lib/fileUnload'

    function swapArray(arr, index1, index2) {
        arr[index1] = arr.splice(index2, 1, arr[index1])[0]
        return arr
    }

    //前移 将当前数组index索引与前面一个元素互换位置，向数组前面移动一位
    function zIndexDown(arr, index) {
        if (index !== 0) {
            swapArray(arr, index, index - 1)
        }
    }

    //后移 将当前数组index索引与后面一个元素互换位置，向数组后面移动一位
    function zIndexUp(arr, index) {
        if (index + 1 !== arr.length) {
            swapArray(arr, index, index + 1)
        }
    }


    export default {
        name: "avatarUploadImgListWrapper",
        props: {
            value: String
        },
        data() {
            return {
                fileList: []
            }
        },
        methods: {
            handlerFile(e) {
                const files = e.target.files
                let len = files.length
                let flLen = this.fileList.length
                for (let i = 0; i < len; i++) {
                    this.fileList.push({
                        loading: true,
                        bigShow: false,
                        url: ''
                    })
                    let index = flLen + i
                    fileUpload(files[i]).then(res => {
                        this.fileList[index].loading = false
                        this.fileList[index].url = this.$root.FILE_PATH + res.url
                    })
                }
            },
            againUploadFile(item) {
                let inputFileDom = document.createElement('input')
                inputFileDom.type = 'file'
                inputFileDom.style.display = 'none'
                document.body.appendChild(inputFileDom)
                inputFileDom.onchange = e => {
                    const file = e.target.files[0]
                    document.body.removeChild(inputFileDom)
                    item.loading = true
                    fileUpload(file).then(res => {
                        item.loading = false
                        item.url = this.$root.FILE_PATH + res.url
                    })
                }
                inputFileDom.click()
            },
            removeItem(index) {
                this.fileList.splice(index, 1)
            },
            zIndexUp(index) {
                zIndexUp(this.fileList, index)
            },
            zIndexDown(index) {
                zIndexDown(this.fileList, index)
            }
        }
    }
</script>
<style lang="scss" scoped>
    .upload-img-list-wrapper {
        display: flex;
        flex-wrap: wrap;
        $size: 100px;

        .item {
            position: relative;
            width: $size;
            height: $size;
            border: 1px solid #ccc;
            margin: 0 10px 10px 0;
            border-radius: 5px;

            .file-input {
                position: relative;
                width: 100%;
                height: 100%;
                overflow: hidden;
                border-radius: 5px;
            }

            &.add-file {
                background: url("data:image/svg+xml,%3Csvg viewBox='0 0 1024 1024' xmlns='http://www.w3.org/2000/svg' %3E%3Cpath d='M544 128h-64v352H128v64h352v352h64V544h351.936v-64H544z' fill='%23999'/%3E%3C/svg%3E") no-repeat center center;
                background-size: 70%;
                transition: all .3s;

                &:hover {
                    border-color: #999;
                }
            }

            input[type=file] {
                position: absolute;
                width: 200%;
                height: 200%;
                top: -20px;
                left: -20px;
                margin: 0;
                padding: 0;
                opacity: 0;
                cursor: pointer;
            }

            .img {
                width: 100%;
                height: 100%;
                display: flex;
                align-items: center;
                justify-content: center;
                overflow: hidden;
                border-radius: 5px;
            }

            img {
                display: block;
                width: 100%;
            }

            .big-wrapper-img {
                position: absolute;
                top: calc(100% + 10px);
                width: 300%;
                background-color: #fff;
                box-shadow: 0 0 10px #ccc;
                padding: 10px;

                &:after {
                    position: absolute;
                    top: -20px;
                    left: 30px;
                    content: "";
                    width: 0;
                    height: 0;
                    background-color: transparent;
                    border: 10px solid transparent;
                    border-bottom: 10px solid #fff;
                }
            }

            .close {
                position: absolute;
                z-index: 2;
                right: -10px;
                top: -10px;
                display: block;
                cursor: pointer;
                font-size: 16px;

                &:hover {
                    & + .operate {
                        display: none;
                    }
                }
            }

            .upload {
                @extend .close;
                top: 13px;
                overflow: hidden;
            }

            .loading {
                position: absolute;
                top: 0;
                left: 0;
                right: 0;
                bottom: 0;
                background-color: rgba(0, 0, 0, .3);
                display: flex;
                align-items: center;
                justify-content: center;
                border-radius: 5px;

                &:after {
                    content: "上传中";
                    font-size: 12px;
                    letter-spacing: 2px;
                    color: #fff;
                }
            }

            .operate {
                @extend .loading;
                background-color: rgba(251, 251, 251, .5);
                top: 50%;
                left: 50%;
                right: 50%;
                bottom: 50%;
                overflow: hidden;
                transition: all .1s;

                &:after {
                    display: none;
                }

                & > div {
                    flex: 1;
                    cursor: pointer;
                    color: #fff;
                    text-align: center;
                    height: 50%;
                    display: flex;
                    align-items: center;
                    justify-content: center;
                    border-radius: 5px;
                    vertical-align: middle;
                    transition: background .3s;
                    font-size: 14px;

                    &:hover {
                        background-color: rgba(0, 0, 0, .9);
                    }
                }
            }

            &:hover {
                .operate {
                    top: -1px;
                    left: -1px;
                    right: -1px;
                    bottom: -1px;
                }
            }
        }
    }
</style>
```  
  