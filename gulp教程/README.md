# 1、什么是gulp？

 gulp是前端开发过程中一种基于流的代码构建工具，是自动化项目的构建利器；它不仅能对网站资源进行优化，而且在开发过程中很多重复的任务能够使用正确的工具自动完成；使用它，不仅可以很愉快的编写代码，而且大大提高我们的工作效率。
 
 gulp是基于Nodejs的自动任务运行器， 它能自动化地完成 javascript、coffee、sass、less、html/image、css 等文件的测试、检查、合并、压缩、格式化、浏览器自动刷新、部署文件生成，并监听文件在改动后重复指定的这些步骤。在实现上，她借鉴了Unix操作系统的管道（pipe）思想，前一级的输出，直接变成后一级的输入，使得在操作上非常简单。通过本文，我们将学习如何使用Gulp来改变开发流程，从而使开发更加快速高效。

gulp 和 grunt 非常类似，但相比于 grunt 的频繁 IO 操作，gulp 的流操作，能更快地更便捷地完成构建工作。

### 一、核心概念：流（stream）
 流，简单来说就是建立在面向对象基础上的一种抽象的处理数据的工具。在流中，定义了一些处理数据的基本操作，如读取数据，写入数据等，程序员是对流进行所有操作的，而不用关心流的另一头数据的真正流向。流不但可以处理文件，还可以处理动态内存、网络数据等多种数据形式。

而gulp正是通过流和代码优于配置的策略来尽量简化任务编写的工作。这看起来有点“像jQuery”的方法，把动作串起来创建构建任务。早在Unix的初期，流就已经存在了。流在Node.js生态系统中也扮演了重要的角色，类似于*nix将几乎所有设备抽象为文件一样，Node将几乎所有IO操作都抽象成了stream的操作。因此用gulp编写任务也可看作是用Node.js编写任务。当使用流时，gulp去除了中间文件，只将最后的输出写入磁盘，整个过程因此变得更快。

### 二、特点

#### 易于使用

通过代码优于配置的策略，gulp 让简单的任务简单，复杂的任务可管理。

#### 构建快速

利用 Node.js 流的威力，你可以快速构建项目并减少频繁的 IO 操作。

#### 易于学习

通过最少的 API，掌握 gulp 毫不费力，构建工作尽在掌握：如同一系列流管道。

#### 插件高质

gulp 严格的插件指南确保插件如你期望的那样简洁高质得工作。

### 三、安装

首先确保你已经正确安装了nodejs环境。然后以全局方式安装gulp：

```javascript
npm install -g gulp
```

如果想在安装的时候把gulp写进项目package.json文件的依赖中，则可以加上--save-dev：

```javascript
npm install --save-dev gulp
```
这样就完成了gulp的安装，接下来就可以在项目中应用gulp了。

### 四、gulp的使用
#### 1、建立gulpfile.js文件
gulp也需要一个文件作为它的主文件，在gulp中这个文件叫做gulpfile.js。新建一个文件名为gulpfile.js的文件，然后放到你的项目目录中。之后要做的事情就是在gulpfile.js文件中定义我们的任务了。下面是一个最简单的gulpfile.js文件内容示例，它定义了一个默认的任务。
```javascript
var gulp = require('gulp');
gulp.task('default',function(){
    console.log('hello world');
});
```
####  2 运行gulp任务
要运行gulp任务，只需切换到存放gulpfile.js文件的目录(windows平台请使用cmd或者Power Shell等工具)，然后在命令行中执行gulp命令就行了，gulp后面可以加上要执行的任务名，例如gulp task1，如果没有指定任务名，则会执行任务名为default的默认任务。


# 2、 gulp api
### 一、工作方式
在介绍gulp API之前，我们首先来说一下gulp.js工作方式。在gulp中，使用的是Nodejs中的stream(流)，首先获取到需要的stream，然后可以通过stream的pipe()方法把流导入到你想要的地方，比如gulp的插件中，经过插件处理后的流又可以继续导入到其他插件中，当然也可以把流写入到文件中。所以gulp是以stream为媒介的，它不需要频繁的生成临时文件，这也是我们应用gulp的一个原因。

gulp的使用流程一般是：首先通过gulp.src()方法获取到想要处理的文件流，然后把文件流通过pipe方法导入到gulp的插件中，最后把经过插件处理后的流再通过pipe方法导入到gulp.dest()中，gulp.dest()方法则把流中的内容写入到文件中。例如：

```javascript
var gulp = require('gulp');
gulp.src('script/jquery.js')         // 获取流的api
    .pipe(gulp.dest('dist/foo.js')); // 写放文件的api
```

### 二、globs的匹配规则

我们重点说说gulp用到的globs的匹配规则以及一些文件匹配技巧，我们将会在后面用到这些规则。

gulp内部使用了node-glob模块来实现其文件匹配功能。我们可以使用下面这些特殊的字符来匹配我们想要的文件

### 三、src：获取流

gulp.src()方法正是用来获取流的，但要注意这个流里的内容不是原始的文件流，而是一个虚拟文件对象流(Vinyl files)，这个虚拟文件对象中存储着原始文件的路径、文件名、内容等信息。其语法为：
```javascript
gulp.src(globs[, options]);
```
 globs参数是文件匹配模式(类似正则表达式)，用来匹配文件路径(包括文件名)，当然这里也可以直接指定某个具体的文件路径。当有多个匹配模式时，该参数可以为一个数组;类型为String或 Array。当有多种匹配模式时可以使用数组

```javascript
 //使用数组的方式来匹配多种文件
gulp.src(['js/*.js','css/*.css','*.html'])
```

### 四、dest：写文件

gulp.dest()方法是用来写文件的，其语法为：

```javascript
gulp.dest(path, [, options]);
```

### 五、watch：监听文件 

gulp.watch()用来监视文件的变化，当文件发生变化后，我们可以利用它来执行相应的任务，例如文件压缩等。其语法为

```javascript
gulp.watch(glob[, opts], tasks); 
```

### 六、task：定义任务

```javascript
gulp.task(name[, deps], fn)
```

name 为任务名；

deps 是当前定义的任务需要依赖的其他任务，为一个数组。当前定义的任务会在所有依赖的任务执行完毕后才开始执行。如果没有依赖，则可省略这个参数；

fn 为任务函数，我们把任务要执行的代码都写在里面。该参数也是可选的。

当你定义一个简单的任务时，需要传入任务名字和执行函数两个属性。