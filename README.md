# 简答题
### 1、谈谈对工程化的初步认识，结合之前遇到过的问题说出三个以上工程化能够解决的问题或者带来的价值
&emsp;&emsp;前端工程化指遵循一定的标准和规范，通过工具去提高效率，降低成本的一种手段，主要内容包括脚手架工具开发、自动化构建系统、模块化打包、项目代码规范化、自动化部署。一切以提高效率、降低成本、质量保证的手段都属于工程化。
<br/><br/>主要解决的问题：
<br/>1.传统语言或语法的弊端，例：想使用ES56+的新特性，但是兼容性有问题、想使用Less/Sass/PostCSS增强CSS的编程性，但是运行环境不能直接支持。
<br/>2.无法使用模块化/组件，例：想使用模块化的方式提高项目的可维护性，但是运行环境不能
<br/>3.重复的机械工作，例：部署上线前需要手动压缩代码及资源文件、部署过程需要手动上传代码到服务器。
<br/>4.代码风格统一、质量保证，例:多人协作开发，无法硬性统一大家的代码风格、从仓库中pull回来的代码质量无法保证。
<br/>5.依赖后端服务接口支持，例：部分功能开发时需要等待后端服务接口提前完成。
<br/>6.整体依赖后端项目。
<br/><br/>
### 2、脚手架除了为我们创建项目结构，还有什么更深的意义
&emsp;&emsp;脚手架除了自动的为我们创建项目基础结构，更重要的是对开发者提供项目规范和约定。通常在开发相同的项目类型时都会有相同的约定，例如：相同的组织结构、相同的开发范式、相同的模块依赖、相同的工具配置、相同的基础代码，这就意味着在创建新的项目时有大量重复性的工作组需要完成，脚手架正式为了解决这类问题，让我们快速搭建特定类型项目骨架，然后基于这骨架进行后面的开发工作。
