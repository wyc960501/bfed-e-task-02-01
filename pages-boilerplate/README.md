# 编程题
### Gulp 实现项目自动化构建过程

在项目文件文件内通过如下命令安装 gulp 模块
```
yarn add gulp --dev
```
接着在根目录下创建 gulpfile.js 文件实现项目构建任务，具体如下：
<br/><br/>1、样式编译
<br/> 载入所需 gulp API
```
const {src,dest} = require('gulp')
```
定义 style 私有任务实现 css 文件的编译转换 ，其中通过安装 gulp-sass 插件开发依赖并载入，实现 css 的编译
```
const sass = require('gulp-sass')
const style = () => {
  return src('src/assets/styles/*.scss',{base:'src'})
    .pipe(sass({outputSyle:'expanded'}))
    .pipe(dest('dist'))
}

module.exports = {
  style
}
```
2、脚本编译
<br/>定义 script 私有任务实现 js 文件的编译转换，其中安装 gulp-babel 插件开发依赖并载入和安装 @babel/core、@babel/preset-env模块，实现 js 的编译转换
```
const base = require('gulp-babel')

const script = () => {
  return src('src/assets/scripts/*.js',{base:'src'})
    .pipe(base({presets:['@babel/preset-env']}))
    .pipe(dest('dist'))
}

module.exports = {
  script
}
```
3、模板编译
<br/>定义 page 私有任务实现模板文件的编译转换，其中安装 gulp-swig 插件开发依赖并载入,实现 模板html文件的编译转换
```
const swig = require('gulp-swig')

const = page = () => {
  return src('src/*.html',{base:'src'})
    .pipe(swig())
    .pipe(dest('dist'))
}

module.exports = {
  page
}

```
4、图片转换
<br/> 定义 image 私有任务实现图片转换，其中安装 gulp-imagemin 插件开发依赖并载入，实现 图片转换
```
const imagemin = require('gulp-imagemin')

const = image = () => {
  return src('src/assets/images/**',{base:'src'})
    .pipe(imagemin())
    .pipe(dest('dist'))
}

module.exports = {
  image
}
```
5、字体转换
<br/> 定义 font 私有任务实现实现转换
```
const = font = () => {
  return src('src/assets/fonts/**',{base:'src'})
    .pipe(imagemin())
    .pipe(dest('dist'))
}

module.exports = {
  font
}
```
6、其他文件拷贝
<br/>定义 extra 私有任务实现其他文件的拷贝
```
const extra = () => {
  return src('public/**',{base:'public'})
    .pipe(dest('dist))
}

module.exports = {
  extra
}
```
7、文件清除
<br/> 安装 del 插件开发依赖并载入，定义 clean 私有任务实现相应文件的清除
```
const del = require('del')

const clean = () => {
  return del(['dist'])
}

module.exports = {
  elean
}
 ```
 8、自动加载插件
 <br/>安装 gulp-load-plugins 插件并载入，通过如下实现所有插件自动加载
 ```
 const loadPlugins = require('gulp-load-plugins')
 
 const plugins = loadPlugins()
 ```
9、创建开发服务器实现代码监视变化以及构建
<br/>安装 browser-sync 模块并载入,通过 browseR-sync 的 create 方法自动创建开发服务器，并定义 serve 任务实现代码监视变化以及构建优化任务
```
const browserSync = require('browser-sync')

const bs = browserSync.create()

const serve = () => {
  watch('src/assets/styles/*.scss',style)
  watch('src/assets/scripts/*.js',script)
  watch('src/*.html',page)
  watch('src/assets/images/**',image)
  watch('src/assets/fonts/**',font)
  watch('public/**',extra)
  
  bs.init({
    server:{
      baseDir:'dist',
      routes:{
        '/node_modules':'node_modules'
      }
    }
  })
}

module.exports = {
  serve
}

```
10、useref 文件引用处理 和 文件压缩
<br/> 安装 gulp-useref 插件开发依赖并载入，定义 useref 任务实现引用文件的构建，安装 gulp-htmlmin、gulp-uglify、gulp-clean-css 等压缩插件和 gulp-if 判断插件实现文件压缩
```
cosnt useref = () => {
  return src('dist/*.html',{base:'dist'})
    .pipe(plugins.useref({searchPath:['dist','.']}))
    // html js css
    .pipe(plugins.if(/\.js$/,plugins.uglify()))
    .pipe(plugins.if(/\.css$/,plugins.cleanCss()))
    .pipe(plugins.if(/\.html$/,plugins.htmlmin({
        collapseWhitespace:true,
        minifyCSS:true,
        minifyJS:true
      })))
    .pipe(dest('dist'))
}

module.exports = {
  useref
}
```
