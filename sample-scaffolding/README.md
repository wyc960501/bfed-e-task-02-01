# 编程题
### sample-scaffolding 脚手架实现过程
首先在项目根目录文件夹下通过下面命令
```
yarn init
```
初始化一个package.json文件,并在package.json文件内添加入口文件
```
"main":"cli.js"
```
接着在根目录文件夹下创建cli.js文件，实现脚手架的工作过程，具体如下:
<br/><br/>1.通过命令行交互询问用户问题
<br/><br/>在命令行输入
```
yarn add inquirer
```
安装 inquirer 模块，并在代码中载入
```
const inquirer = require('inquirer')
```
通过 inquirer 的 prompt() 方法向用户发起项目名称的询问
```
inquirer.prompt([
  {
    type: 'input',
    name: 'name',
    message: 'Project name?'
   }
])
```
<br/>2.根据用户回答的结果生成文件
<br/><br/>在命令行输入
```
yarn add ejs
```
安装模板渲染引擎，并在代码中载入 ejs、fs、path等模块
```
const fs = require('fs')
const path = require('path')
const ejs = require('ejs')
```
接着通过 inquirer 的 then() 方法将用户回答的信息通过 ejs 模板引擎渲染到模板文件，并通过 fs 文件系统将模板文件转换到目标目录
```
.then(anwsers => {
  // 模板目录
  const tmplDir = path.join(__dirname,'templates)
  // 目标目录
  const destDir = process.cwd()
  
  fs.readdir(tmplDir,(err,files) => {
    if (err) throw err
    files.forEach(file => {
      // 通过模板引擎渲染文件
      ejs.renderFile(path.join(tmplDir,file),anwsers,(err,result) => {
        if (err) throw err
        // 将结果下入目标文件路径
        fs.writeFileSync(path.join(destDir,file),result)
      })
    })
  })
})
```
