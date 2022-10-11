---
title: vue计算属性之computed 全选示例  
tag: JavaScript,Vue  
---  

```js
/*
    计算属性:vue中对数据进行一些组合与计算的话，可以使用computed(计算属性);
    //例如：获取当前日期，组合
*/
//    组合变成10-1
var vm = new Vue({
    el: '#app',
    data: {

    },
    computed: {
        //默认写法是这样
        time: {
            return new Date().getMonth() + 1 + '-' + new Date().getDate();
        },
    },
});
//下面是另一种常用的写法
var vm = new Vue({
    el: '#app',
    data: {
        month: 10,
        day: 1,
    },
    computed: {
        time： {
            get: function () {
                //默认只有get
                return new Date().getMonth() + 1 + '-' + new Date().getDate();
            },
            set: function (value) {
                //在这里面可以写一些方法控制data中的值；
            }
        },
    },
});
```
### 示例
```html
<div id="box">
    <div>
        <input type="checkbox" v-model="allcheck">全选</div>
    <br>
    <ul>
        <li v-for="(v,index) in list">
            <input type="checkbox" v-model="v.status">
            <label>{{ v.name + '  ' + v.status}}</label>
        </li>
    </ul>
</div>
```
``` js
var list = [
    {
        id: 1,
        name: "小学",
        status: false
    },
    {
        id: 2,
        name: "中学",
        status: false
    },
    {
        id: 3,
        name: "高中",
        status: false
    },
    {
        id: 4,
        name: "大学",
        status: false
    },
    {
        id: 5,
        name: "研究生",
        status: false
    },
    {
        id: 6,
        name: "博士",
        status: false
    }
];
var vm = new Vue({
    el: '#box',
    data: {
        list: list
    },
    computed: {
        allcheck: {
            get: function () {
                var arr = [];
                arr = this.list.filter(function (item) {
                    return !item.status
                });
                if (arr.length == 0) {
                    return true
                }
                console.log(arr)
            },
            set: function (value) {
                console.log(value)
                vm.list.forEach(function (item) {
                    item.status = value;
                });
                value = !value
            }
        }
    },
    methods: {

    }
});
```
``` css
#box {
    width: 600px;
    margin: 50px auto;
}
ul {
    list-style: none;
    padding: 0;
    margin: 0;
}
input[type="checkbox"] {
    width: 17px;
    height: 17px;
}
```  
  