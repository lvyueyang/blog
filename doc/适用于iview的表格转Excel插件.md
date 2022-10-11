---
title: 适用于iview的表格转Excel插件  
tag: Vue,ES6  
---  

>在网上找的一个表格转excel插件，经过修改后使其适用于iview中的table组件

```js
let idTmr;
const getExplorer = () => {
    let explorer = window.navigator.userAgent;
    //ie 
    if (explorer.indexOf("MSIE") >= 0) {
        return 'ie';
    }
    //firefox 
    else if (explorer.indexOf("Firefox") >= 0) {
        return 'Firefox';
    }
    //Chrome
    else if (explorer.indexOf("Chrome") >= 0) {
        return 'Chrome';
    }
    //Opera
    else if (explorer.indexOf("Opera") >= 0) {
        return 'Opera';
    }
    //Safari
    else if (explorer.indexOf("Safari") >= 0) {
        return 'Safari';
    }
}

const method = (ref,name) => { 

    //整个表格拷贝到EXCEL中
    if (getExplorer() == 'ie') {
        let curTbl = ref;
        let oXL = new ActiveXObject("Excel.Application");

        //创建AX对象excel 
        let oWB = oXL.Workbooks.Add();
        //获取workbook对象 
        let xlsheet = oWB.Worksheets(1);
        //激活当前sheet 
        let sel = document.body.createTextRange();
        sel.moveToElementText(curTbl);
        //把表格中的内容移到TextRange中 
        sel.select;
        //全选TextRange中内容 
        sel.execCommand("Copy");
        //复制TextRange中内容  
        xlsheet.Paste();
        //粘贴到活动的EXCEL中       
        oXL.Visible = true;
        //设置excel可见属性

        try {
            let fname = oXL.Application.GetSaveAsFilename("Excel.xls", "Excel Spreadsheets (*.xls), *.xls");
        } catch (e) {
            print("Nested catch caught " + e);
        } finally {
            oWB.SaveAs(fname);

            oWB.Close(savechanges = false);
            //xls.visible = false;
            oXL.Quit();
            oXL = null;
            // 结束excel进程，退出完成
            window.setInterval("Cleanup();", 1);
            idTmr = window.setInterval("Cleanup();", 1);

        }

    } else {
        tableToExcel(ref,name)
    }
}

const Cleanup = () => {
    window.clearInterval(idTmr);
}

const tableToExcel = (function() {
    // 编码要用utf-8不然默认gbk会出现中文乱码
    let uri = 'data:application/vnd.ms-excel;base64,',
        template = '<html xmlns:o="urn:schemas-microsoft-com:office:office" xmlns:x="urn:schemas-microsoft-com:office:excel" xmlns="http://www.w3.org/TR/REC-html40"><head><meta charset="UTF-8"><!--[if gte mso 9]><xml><x:ExcelWorkbook><x:ExcelWorksheets><x:ExcelWorksheet><x:Name>{worksheet}</x:Name><x:WorksheetOptions><x:DisplayGridlines/></x:WorksheetOptions></x:ExcelWorksheet></x:ExcelWorksheets></x:ExcelWorkbook></xml><![endif]--></head><body><table>{table}</table></body></html>',
        base64 = function(s) {
            return window.btoa(unescape(encodeURIComponent(s)));
        }, 
        format = (s, c) => {
            return s.replace(/{(\w+)}/g,
                (m, p) => {
                    return c[p];
                })
        }
    return (table, name) => {
        let ctx = {
            worksheet: name,
            table
        }

        //创建下载
        let link = document.createElement('a');
        link.setAttribute('href', uri + base64(format(template, ctx)));
        link.setAttribute('download', name); 

        // window.location.href = uri + base64(format(template, ctx))
        link.click();
    }
})()

export default (theadData, tbodyEle, dataname = 'Worksheet') => {
    // 写入key过滤不显示的td
    let thArr = [];
    // 建立节点
    let table = document.createElement('table');
    let thead = document.createElement('thead');
    let tbody = tbodyEle.$el.getElementsByClassName('ivu-table-tbody')[0].cloneNode(true);
    
    //  建立thead中的tr
    let thTr = document.createElement('tr');
    //  遍历写入th表头
    for(let i of theadData){
        thArr.push(i.key);
        let th = document.createElement('th');
        let text = document.createTextNode(i.title);
        th.appendChild(text);
        thTr.appendChild(th);
    }
    
    thead.appendChild(thTr);
    table.appendChild(thead);
    table.appendChild(tbody)
    console.log(table)
    method(table.innerHTML, dataname);
}
```
## 示例
``` html
<template>
  <div>
    <Table :columns="columns" :data="data" size="small" ref="table"></Table>
    <br>
    <Button type="primary" size="large" @click="exportData()">
      <Icon type="ios-download-outline"></Icon> Export source data</Button>
  </div>
</template>
<script>
import excel from './tableToExcel.js'
export default {
  name: 'HelloWorld',
  data() {
    return {
      columns: [{
          title: '序号',
          type: 'index',
          width: 60,
          align: 'center'
        },
        {
          title: '姓名',
          width: 100,
          key: 'xingming'
        },
        {
          title: '个人账号',
          key: 'grzh'
        },
        {
          title: '证件号码',
          key: 'zjhm'
        },
        {
          title: '未通过原因',
          key: 'cwxx'
        }
      ],
      data: [{
        xingming: '张三',
        grzh: '11231',
        zjhm: '123123123123123',
        cwxx: '未通过原因',
      }, {
        xingming: '张三',
        grzh: '11231',
        zjhm: '123123123123123',
        cwxx: '未通过原因',
      }]
    }
  },
  methods: {
    exportData() {
      excel(this.columns, this.$refs.table, '错误报告');
    }
  }
}

</script>
```  
  