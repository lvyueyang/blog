---
title: node egg.js使用superagent做文件转发  
tag: Node,文件上传,egg  
---  

``` javascript
// app/controller/file.js
const Controller = require('egg').Controller;
const fs = require('fs')
const request = require('superagent')
const sendToWormhole = require('stream-wormhole')
const toArray = require('stream-to-array');
const path = require('path');
const uuid = require('uuid/v1');

class FileController extends Controller {
    async file() {
        const { ctx, app } = this;
        // 获取上传的文件
        let stream;
		try {
			stream = await ctx.getFileStream();
		} catch (e) {
            console.error('文件不存在或者文件错误');
		}
		if (!stream) {
            ctx.throw(403,'文件不存在或者文件错误')
			return false;
        }
        const nameid = uuid().replace(/-/g, '');
        const filename = nameid + '.' + stream.filename.toLowerCase().split('.').pop();
        // 文件暂时存在 app/public 文件夹下
        const target = path.join(this.config.baseDir, 'app/public', filename);
        const url = '上传地址';
        // 使用 superagent 上传
        try {
            // 转化stream
			const parts = await toArray(stream);
            let buf = Buffer.concat(parts);
            // 写入文件保存至本地
            fs.writeFileSync(target, buf);
            // 上传
			const res = await request
				.post(url)
				.attach('file', target, filename)
            ctx.body = res.text;
		} catch (err) {
            // 必须将上传的文件流消费掉，要不然浏览器响应会卡死
            await sendToWormhole(stream);
            ctx.throw(500,'文件上传出错');
        }
        
		// 因为只做临时保存，在上传完毕后删除文件
		fs.unlink(target, function (err) {
			if (!err) {
				console.log('文件已删除：', target);
			}
		});
    }
}
module.exports = FileController;

```

**地址资源链接**  
superagent官方文档
> [http://visionmedia.github.io/superagent/ ](http://visionmedia.github.io/superagent/ ) 

egg文件上传参考文档  
> [https://eggjs.org/zh-cn/basics/controller.html#%E8%8E%B7%E5%8F%96%E4%B8%8A%E4%BC%A0%E7%9A%84%E6%96%87%E4%BB%B6](https://eggjs.org/zh-cn/basics/controller.html#%E8%8E%B7%E5%8F%96%E4%B8%8A%E4%BC%A0%E7%9A%84%E6%96%87%E4%BB%B6)  
  