---
title: 观察者模式 Observer  
tag: ES6,小示例,工具函数  
---  

``` js
export default class Observer {
    constructor() {
        this.observers = {}
    }

    on(name, cb) {
        if (!this.observers[name]) {
            this.observers[name] = []
        }
        this.observers[name].push(cb)
    }

    once(name, cb) {
        const wrapper = (...args) => {
            cb(...args)
            this.off(name, wrapper)
        }
        this.on(name, wrapper)
    }

    off(name, cb) {
        if (!this.observers[name]) {
            return
        }

        if (Array.isArray(this.observers[name])) {
            const index = this.observers[name].indexOf(cb)
            if (index !== -1) {
                this.observers[name].splice(index, 1)
            }
        }

        if (typeof this.observers[name] === 'function') {
            delete this.observers[name]
        }
    }

    emit(name, ...args) {
        const observerItem = this.observers[name]
        if (!observerItem) {
            return
        }
        if (Array.isArray(observerItem)) {
            this.observers[name].forEach(cb => {
                cb && cb(...args)
            })
        }
        if (typeof observerItem === 'function') {
            this.observers[name](...args)
        }
    }
}
```  
  