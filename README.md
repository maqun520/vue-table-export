# vue-table-export
1.安装相关依赖
npm install --save xlsx file-saver
2.导入相关插件
const FileSaver  = require("file-saver")
const XLSX   = require("xlsx")
3.调用相关的方法

var wb = XLSX.utils.table_to_book(document.querySelector("#tableBox"))
var wbout = XLSX.write(wb, { bookType: 'xlsx', bookSST: true, type: 'array' })
try {
  FileSaver.saveAs(new Blob([wbout], { type: 'application/octet-stream' }), 'sheetjs.xlsx')
} catch (e) { if (typeof console !== 'undefined') console.log(e, wbout) }
4.分页的数据导出
// 执行下载
async activeExportOut(){
  // this.ableExportOut = true //设置可以下载
  this.oldtableData = this.tableData //保存起就数据
  await this.setData()
  this.exportOut()
},
setData(){
  this.tableData = test //赋值新数据       
},
//下载表格
exportOut(){
   var wb = XLSX.utils.table_to_book(document.querySelector("#tableBox"))
   var wbout = XLSX.write(wb, { bookType: 'xlsx', bookSST: true, type: 'array' })
   try {
       FileSaver.saveAs(new Blob([wbout], { type: 'application/octet-stream' }), 'sheetjs.xlsx')
   } catch (e) { if (typeof console !== 'undefined') console.log(e, wbout) }
 
  //  this.ableExportOut = false //设置不可下载
   this.tableData = this.oldtableData //回复原来说的数据
   return wbout
}
