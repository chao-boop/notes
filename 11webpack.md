# webpack 一个很流行的构建工具   在工作中很少使用 但是后面的框架里面的工程搭建包含了webpack 
因为在浏览器端，开发状态和运行状态的侧重点不一样 利用webpack将开发时的文件进行打包
常见的构建工具：- **webpack**     - grunt - gulp  - browserify  - fis  - 其他  
## webpack的安装和使用
> webpack官网：https://www.webpackjs.com/
> 目前的最新版本：webpack4

webpack是基于模块化的打包（构建）工具，它把一切视为模块
它通过一个开发时态的入口模块为起点，分析出所有的依赖关系，然后经过一系列的过程（压缩、合并），最终生成运行时态的文件。

    webpack的特点：
        - **为前端工程化而生**：webpack致力于解决前端工程化，特别是浏览器端工程化中遇到的问题，让开发者集中注意力编写业务代码，而把工程化过程中的问题全部交给webpack来处理
        - **简单易用**：支持零配置，可以不用写任何一行额外的代码就使用webpack
        - **强大的生态**：webpack是非常灵活、可以扩展的，webpack本身的功能并不多，但它提供了一些可以扩展其功能的机制，使得一些第三方库可以融于到webpack中
        - **基于nodejs**：由于webpack在构建的过程中需要读取文件，因此它是运行在node环境中的
        - **基于模块化**：webpack在构建过程中要分析依赖关系，方式是通过模块化导入语句进行分析的，它支持各种模块化标准，包括但不限于CommonJS、ES6 Module

### webpack的安装

webpack通过npm安装，它提供了两个包：
  - webpack：核心包，包含了webpack构建过程中要用到的所有api
  - webpack-cli：提供一个简单的cli命令，它调用了webpack核心包的api，来完成构建过程

###  安装方式：- 注意 安装时应该是将webpack安装在运行环境 因为它只是为了将运行环境的文件打包到生产环境  ## 安装依赖到开发环境：npm i --save-dev 包名 或 npm i -D 包名
                                                                                             
- 全局安装：可以全局使用webpack命令，但是无法为不同项目对应不同的webpack版本
- **本地安装**：推荐，每个项目都使用自己的webpack版本进行构建


###  注意   默认情况下，webpack会以```./src/index.js```作为入口文件分析依赖关系，打包结果会放在```./dist/main.js```文件中
所以要建立一个scr文件夹 里面键一个index.js文件 webpack会以此为入口进行打包
通过--mode选项可以控制webpack的打包结果的运行环境

### webpack同时支持commonjs和es6模块化 因此需要互相操作时webpack是如何处理的
它可以兼容不同的导入或导出方式 比如用commonjs导出。es6导入 或者反之
然而 
代码编写最忌讳的是精神分裂，选择一个合适的模块化标准，然后贯彻整个开发阶段
所以尽量避免

### 如何打包
    npx webpack 全局打包
    npx webpack --mode=development 打包到开发环境下 
                webpack --mode=development --watch 一直监听 有改动就自动打包到生产环境下 不需要在频繁操作
    npx webpack --mode=production  打包到生产环境下
可以用脚本 方便调用：
 "scripts": {
        "dev": "webpack --mode=development --watch",
        "build": "webpack --mode=production"
    },
### webpack的配置文件
webpack提供的cli支持很多的参数，例如```--mode```，但更多的时候，我们会使用更加灵活的配置文件来控制webpack的行为
            默认情况下，webpack会读取```webpack.config.js```文件作为配置文件 一般在根目录下新建，但也可以通过CLI参数```--config```来指定某个配置文件
- 配置文件中通过CommonJS模块导出一个对象，对象中的各种属性对应不同的webpack配置  注意必须是commontjs导出 因为打包过程中会运行这个文件 打包前的其他文件是不会运行的 所以不会报错
**注意：配置文件中的代码，必须是有效的node代码**
    当命令行参数与配置文件中的配置出现冲突时，以命令行参数为准。
**基本配置：**
        1. mode：编译模式，字符串，取值为development或production，指定编译结果代码运行的环境，会影响webpack对编译结果代码格式的处理
        2. entry：配置的是入口文件 chunk   如果这样写 entry:"./src/index.js"  也会转化为下面的写法
                    {
                        main:"./src/index.js"     默认情况就是这样写的 一个是chunk的 名字 一个是文件相对位置
                    }

                    但是如果有多个chunk是会出现问题 因为文件只有每次都会创建固定的名字一样的文件  那么filename可以这样写  这样会以入口chunk的名字创建一个出口文件名  
                    [name]左右可以随便加什么 总之[name]会替换为出口文件的名字
                    但是我们会这样写[name][hash].js 加一个hash值 使得每次都是一个新的名字 因为浏览器访问js文件时如果发现名字一样就会拿缓存里的 不会用跟新了的js文件  所以每次生成一个新的文件名 左右两边也是随便加什么都可以  
                    可以规定hash的位数 [hash:5] 表示取五位
                    但是是有一个问题 就是一个js文件改了 打包后所有的文件名都会改变 所以可以使用chunkhash 这样可以只让更改了的文件hash值发生变化 所以把hash替换成chunkhash 
        3. output：出口，，指定编译结果存放位置
                    - filename:"[name][chunkhash:5].js"   //配置的合并的js文件的规则  如果直接写一个文件名就是将合并的js模板存储在该文件内  产生的文件名会放在path规定的文件夹下
                    - path: //必须配置一个绝对路径，表示资源放置的文件夹  默认是dist文件的绝对路径  但是不同操作系统路径写法不一样 所以可以这样 
                                                                        path:path.resclve(__dirname,"target") 放置在根目录的target内 



                > node内置模块 - path: https://nodejs.org/dist/latest-v12.x/docs/api/path.html
                **出口**
                这里的出口是针对资源列表的文件名或路径的配置
                出口通过output进行配置
                **入口**
                **入口真正配置的是chunk**
                入口通过entry进行配置
                规则：
                - name：chunkname
                - hash: 总的资源hash，通常用于解决缓存问题
                - chunkhash: 使用chunkhash
                - id: 使用chunkid，不推荐

### devtoo配置  关于打包后调试代码困难的问题 

source map实际上是一个配置，配置中不仅记录了所有源码内容，还记录了和转换后的代码的对应关系
1. source map 应在开发环境中使用，作为一种调试手段
2. source map 不应该在生产环境中使用，source map的文件一般较大，不仅会导致额外的网络传输，还容易暴露原始代码。即便要在生产环境中使用source map，用于调试真实的代码运行问题，也要做出一些处理规避网络传输和代码暴露的问题。
### webpack中的source map 源码地图
        module.exports{
            mode:"production",
            devtool:"none"     //生产环境默认是none  开发环境 devtool默认是eval
                
        }
使用 webpack 编译后的代码难以调试，可以通过 devtool 配置来**优化调试体验**
具体的配置见文档：https://www.webpackjs.com/configuration/devtool/

### webpack做的事情，仅仅是分析出各种模块的依赖关系，然后形成资源列表，最终打包生成到指定的文件中。 更多的功能需要借助webpack loaders和webpack plugins完成。

#### loader  本质上是一个函数，它的作用是将某个源码字符串转换成另一个源码字符串返回。
loader函数的将在模块解析的过程中被调用，以得到最终的源码。
**loader配置：**
  **完整配置**
```js
module.exports = {
    module: { 
        rules: [ //模块匹配规则，可以存在多个规则  
            { //每个规则是一个对象
                test: /\.js$/, //匹配的模块正则  
                use: [  "" //匹配到后应用的规则模块 当遇到text规则符合的文件 然后交给谁来处理 
                             {  //其中一个规则
                        loader: "模块路径", //loader模块的路径，该字符串会被放置到require中
                        options: { //向对应loader传递的额外参数

                                     }
                                }
                     ]
                 }
        ]
    }
}
```
  **简化配置**
```js
module.exports = {
    module: { //针对模块的配置，目前版本只有两个配置，rules、noParse
        rules: [ //模块匹配规则，可以存在多个规则
            { //每个规则是一个对象
                test: /\.js$/, //匹配的模块正则
                use: ["模块路径1", "模块路径2"]//loader模块的路径，该字符串会被放置到require中
            }
        ]
    }
}
```

#### plugin   loader的功能定位是转换代码，而一些其他的操作难以使用loader完成，比如：
                    当webpack生成文件时，顺便多生成一个说明描述文件
                    当webpack编译启动时，控制台输出一句话表示webpack启动了
                    当xxxx时，xxxx
                    这种类似的功能需要把功能嵌入到webpack的编译流程中，而这种事情的实现是依托于plugin的


plugin的**本质**是一个带有apply方法的对象

```js
var plugin = {
    apply: function(compiler){
        
    }
}
```
通常，习惯上，我们会将该对象写成构造函数的模式

```js
class MyPlugin{
    apply(compiler){

    }
}
```
###  区分生产和开发环境  单独配置文件

有些时候，我们需要针对生产环境和开发环境分别书写webpack配置

为了更好的适应这种要求，webpack允许配置不仅可以是一个对象，还可以是一个**函数**

```js
module.exports = env => {
    return {
        //配置内容
    }
}
```

在开始构建时，webpack如果发现配置是一个函数，会调用该函数，将函数返回的对象作为配置内容，因此，开发者可以根据不同的环境返回不同的对象
在调用webpack函数时，webpack会向函数传入一个参数env，该参数的值来自于webpack命令中给env指定的值，例如

```shell
npx webpack --env abc # env: "abc"

npx webpack --env.abc # env: {abc:true}
npx webpack --env.abc=1  # env： {abc:1}
npx webpack --env.abc=1 --env.bcd=2 # env: {abc:1, bcd:2}
```
这样一来，我们就可以在命令中指定环境，在代码中进行判断，根据环境返回不同的配置结果。

### 其他细节配置

- context

```js
context: path.resolve(__dirname, "app")
```
该配置会影响入口和loaders的解析，入口和loaders的相对路径会以context的配置作为基准路径，这样，你的配置会独立于CWD（current working directory 当前执行路径）

- output

- library

```js
library: "abc"
```

这样一来，打包后的结果中，会将自执行函数的执行结果暴露给abc 

- libraryTarget

```js
libraryTarget: "var"
```
该配置可以更加精细的控制如何暴露入口包的导出结果

其他可用的值有：
            - var：默认值，暴露给一个普通变量
            - window：暴露给window对象的一个属性
            - this：暴露给this的一个属性
            - global：暴露给global的一个属性
            - commonjs：暴露给exports的一个属性
            - 其他：https://www.webpackjs.com/configuration/output/#output-librarytarget

- target

```js
target:"web" //默认值
```

设置打包结果最终要运行的环境，常用值有
- web: 打包后的代码运行在web环境中
- node：打包后的代码运行在node环境中
- 其他：https://www.webpackjs.com/configuration/target/

-  module.noParse
```js
noParse: /jquery/
```
不解析正则表达式匹配的模块，通常用它来忽略那些大型的单模块库，以提高**构建性能**

-  resolve
resolve的相关配置主要用于控制模块解析过程

-  modules

```js
modules: ["node_modules"]  //默认值
```
当解析模块时，如果遇到导入语句，```require("test")```，webpack会从下面的位置寻找依赖的模块

1. 当前目录下的```node_modules```目录
2. 上级目录下的```node_modules```目录
3. ...

- extensions
```js
extensions: [".js", ".json"]  //默认值
```

当解析模块时，遇到无具体后缀的导入语句，例如```require("test")```，会依次测试它的后缀名

- test.js
- test.json
- alias

```js
alias: {
  "@": path.resolve(__dirname, 'src'),
  "_": __dirname
}
```
有了alias（别名）后，导入语句中可以加入配置的键名，例如```require("@/abc.js")```，webpack会将其看作是```require(src的绝对路径+"/abc.js")```。

在大型系统中，源码结构往往比较深和复杂，别名配置可以让我们更加方便的导入依赖

- externals

```js
externals: {
    jquery: "$",
    lodash: "_"
}
```
从最终的bundle中排除掉配置的配置的源码，例如，入口模块是
```js
//index.js
require("jquery")
require("lodash")
```

生成的bundle是：

```js
(function(){
    ...
})({
    "./src/index.js": function(module, exports, __webpack_require__){
        __webpack_require__("jquery")
        __webpack_require__("lodash")
    },
    "jquery": function(module, exports){
        //jquery的大量源码
    },
    "lodash": function(module, exports){
        //lodash的大量源码
    },
})
```

但有了上面的配置后，则变成了

```js
(function(){
    ...
})({
    "./src/index.js": function(module, exports, __webpack_require__){
        __webpack_require__("jquery")
        __webpack_require__("lodash")
    },
    "jquery": function(module, exports){
        module.exports = $;
    },
    "lodash": function(module, exports){
        module.exports = _;
    },
})
```

这比较适用于一些第三方库来自于外部CDN的情况，这样一来，即可以在页面中使用CDN，又让bundle的体积变得更小，还不影响源码的编写

- stats
stats控制的是构建过程中控制台的输出内容


### webpack的常用扩展 webpack的第三方库解决了webpack使用过程中的很多问题

去npmjs.com 官网查找

- 清除输出目录 重新打包后 要手动删除原来的文件比较麻烦  clean-webpack-plugin 插件
            使用方法  ：const { CleanWebpackPlugin } = require('clean-webpack-plugin');
                         module.exports = {
                                             plugins: [
                                    
                                                     new CleanWebpackPlugin(),
                                                     ],

                                                };
                            
                        

- 自动生成页面 html-webpack-plugin
- 复制静态资源 copy-webpack-plugin
- 开发1服务器 解决每次运行代码都要打包的问题 webpack-dev-server
    在**开发阶段**，目前遇到的问题是打包、运行、调试过程过于繁琐，回顾一下我们的操作流程：
            1. 编写代码
            2. 控制台运行命令完成打包
            3. 打开页面查看效果
            4. 继续编写代码，回到步骤2

    并且，我们往往希望把最终生成的代码和页面部署到服务器上，来模拟真实环境  为了解决这些问题，webpack官方制作了一个单独的库：**webpack-dev-server**
    它**既不是plugin也不是loader**  
    先来看看它怎么用
                    1. 安装
                    2. 执行```webpack-dev-server```命令  可以写在package配置文件内的script内方便执行
                    也可以在webpack配置文件上加  devServer:{open:true} 让其自动打开



                    ```webpack-dev-server```命令几乎支持所有的webpack命令参数，如```--config```、```-env```等等，你可以把它当作webpack命令使用
                    这个命令是专门为开发阶段服务的，真正部署的时候还是得使用webpack命令
    当我们执行```webpack-dev-server```命令后，它做了以下操作：
                                                    1. 内部执行webpack命令，传递命令参数
                                                    2. 开启watch
                                                    3. 注册hooks：类似于plugin，webpack-dev-server会向webpack中注册一些钩子函数，主要功能如下：
                                                            1. 将资源列表（aseets）保存起来
                                                            2. 禁止webpack输出文件
                                                            4. 用express开启一个服务器，监听某个端口，当请求到达后，根据请求的路径，给予相应的资源内容

                            **配置**
                            针对webpack-dev-server的配置，参考：https://www.webpackjs.com/configuration/dev-server/
                            常见配置有：
                                - port：配置监听端口
                                - proxy：配置代理，常用于跨域访问
                                - stats：配置控制台输出内容


- 普通文件处理  
                        file-loader: 生成依赖的文件到输出目录，然后将模块文件设置为：导出一个路径\
                        ```js
                        //file-loader
                        function loader(source){
                            // source：文件内容（图片内容 buffer）
                            // 1. 生成一个具有相同文件内容的文件到输出目录
                            // 2. 返回一段代码   export default "文件名"
                        }
                        ```
                        url-loader：将依赖的文件转换为：导出一个base64格式的字符串

                        ```js
                        //file-loader
                        function loader(source){
                            // source：文件内容（图片内容 buffer）
                            // 1. 根据buffer生成一个base64编码
                            // 2. 返回一段代码   export default "base64编码"
                        }
                        ```
- 解决路径问题
        使用file-loader或url-loader时，可能会遇到一个非常有趣的问题
                比如，通过webpack打包的目录结构如下：
                                ```yaml
                                dist
                                    |—— img
                                        |—— a.png  #file-loader生成的文件
                                    |—— scripts
                                        |—— main.js  #export default "img/a.png"
                                    |—— html
                                        |—— index.html #<script src="../scripts/main.js" ></script>
                                ```
    这种问题发生的根本原因：模块中的路径来自于某个loader或plugin，当产生路径时，loader或plugin只有相对于dist目录的路径，并不知道该路径将在哪个资源中使用，从而无法确定最终正确的路径
    面对这种情况，需要依靠webpack的配置publicPath解决

- webpack内置插件 webpack自带的
            所有的webpack内置插件都作为webpack的静态属性存在的，使用下面的方式即可创建一个插件对象

            ```js
            const webpack = require("webpack")
            new webpack.插件名(options)
            ```

    1. DefinePlugin 全局常量定义插件，使用该插件通常定义一些常量值，例如：

            ```js
            new webpack.DefinePlugin({
                PI: `Math.PI`, // PI = Math.PI
                VERSION: `"1.0.0"`, // VERSION = "1.0.0"
                DOMAIN: JSON.stringify("duyi.com")
            })
            ```

        这样一来，在源码中，我们可以直接使用插件中提供的常量，当webpack编译完成后，会自动替换为常量的值

    2. BannerPlugin 它可以为每个chunk生成的文件头部添加一行注释，一般用于添加作者、公司、版权等信息

                ```js
                new webpack.BannerPlugin({
                banner: `
                hash:[hash]
                chunkhash:[chunkhash]
                name:[name]
                author:yuanjin
                corporation:duyi
                `
                })
                ```

    3. ProvidePlugin  自动加载模块，而不必到处 import 或 require 
                ```js
                new webpack.ProvidePlugin({
                $: 'jquery',
                _: 'lodash'
                })
                ```

                然后在我们任意源码中：
                ```js
                $('#item'); // <= 起作用
                _.drop([1, 2, 3], 2); // <= 起作用
                ```
# css工程化  
主要是解决三个问题 
## 解决css文件细分问题   对多个css文件进行处理
  利用webpack拆分css 要拆分css就必须把css当成js那样的模块 然而webpack本身只能读取css文件内容 所以需要利用loader将css文件代码转换为js代码
    - css-loader  作用是将css代码转化为js代码  它的处理原理极其简单：将css代码作为字符串导出
            其作用：
        1. 将css文件的内容作为字符串导出
        2. 将css中的其他依赖作为require导入，以便webpack分析依赖
    - style-loader  由于css-loader仅提供了将css转换为字符串导出的能力，剩余的事情要交给其他loader或plugin来处理   style-loader可以将css-loader转换后的代码进一步处理，将       css-loader导出的字符串加入到页面的style元素中


    - 如果css文件有其他资源需要导入 比如图片资源 需要在写一个规则rule
     rules: [ //模块匹配规则，可以存在多个规则  
            {test: /\.css$/,use: ["style-loader","css-loader"] }  //执行顺序是从右往左 
            {test: /\.png$/,  use: "file-loader" }  //也可以用url-loader
                ]
## 解决重复样式问题
### css in js
### 预编译器 目前，最流行的预编译器有LESS和SASS，由于它们两者特别相似，因此仅学习一种即可（本课程学习LESS）
less官网：http://lesscss.org/
less中文文档1（非官方）：http://lesscss.cn/
less中文文档2（非官方）：https://less.bootcss.com/  更好一点
sass官网：https://sass-lang.com/
sass中文文档1（非官方）：https://www.sass.hk/  更好一点
sass中文文档2（非官方）：https://sass.bootcss.com/

原理可知，要使用LESS，必须要安装LESS编译器
LESS编译器是基于node开发的，可以通过npm下载安装
npm i -D less
安装好了less之后，它提供了一个CLI工具lessc，通过该工具即可完成编译
lessc less代码文件 编译后的文件

试一试:
新建一个index.less文件，编写内容如下：
// less代码
@red: #f40;

.redcolor {
    color: @red;
}
                                                        运行命令：
                                                            lessc index.less index.css  
可以看到编译之后的代码：
.redcolor {
  color: #f40;
}
LESS的基本使用
具体的使用见文档：https://less.bootcss.com/
变量 混合 嵌套 运算 函数 作用域 注释 导入

### webpack中使用 
安装一个less-loader
配置test就可以 {test:/\.less$/,use:["style-loader","css-loader","less-loader"]}  


## 解决类名冲突问题
第三方提出了一些解决方案 
        1.命名约定：就是提供一种命名标准，来解决冲突，常见的标准有：BEM OOCSS AMCSS 等等
        2.css-in-js  在js中书写样式
        3.css.module
### BEM 类名规约
BEM全称是：**B**lock **E**lement **M**odifi
三个部分的具体含义为：
- **Block**：页面中的大区域，表示最顶级的划分，例如：轮播图(```banner```)、布局(```layout```)、文章(```article```)等等
- **element**：区域中的组成部分，例如：轮播图中的横幅图片(```banner__img```)、轮播图中的容器（```banner__container```）、布局中的头部(```layout__header```)、文章中的标题(```article_title```)
- **modifier**：可选。通常表示状态，例如：处于展开状态的布局左边栏（```layout__left_expand```）、处于选中状态的轮播图小圆点(```banner__dot_selected```)

在某些大型工程中，如果使用BEM命名法，还可能会增加一个前缀，来表示类名的用途，常见的前缀有：

- **l**: layout，表示这个样式是用于布局的
- **c**: component，表示这个样式是一个组件，即一个功能区域
- **u**: util，表示这个样式是一个通用的、工具性质的样式
- **j**: javascript，表示这个样式没有实际意义，是专门提供给js获取元素使用的
### css-in-js  css in js 的核心思想是：用一个JS对象来描述样式，而不是css样式表
        例如下面的对象就是一个用于描述样式的对象：
                            ```js
                            const styles = {
                                backgroundColor: "#f40",
                                color: "#fff",
                                width: "400px",
                                height: "500px",
                                margin: "0 auto"
                            }
                            ```

        由于这种描述样式的方式**根本就不存在类名**，自然不会有类名冲突
            至于如何把样式应用到界面上，不是它所关心的事情，你可以用任何技术、任何框架、任何方式将它应用到界面。
> 后续学习的vue、react都支持css in js，可以非常轻松的应用到界面
css in js的特点：

- **绝无冲突的可能**：由于它根本不存在类名，所以绝不可能出现类名冲突
- **更加灵活**：可以充分利用JS语言灵活的特点，用各种招式来处理样式
- **应用面更广**：只要支持js语言，就可以支持css in js，因此，在一些用JS语言开发移动端应用的时候非常好用，因为移动端应用很有可能并不支持css
- **书写不便**：书写样式，特别是公共样式的时候，处理起来不是很方便
- **在页面中增加了大量冗余内容**：在页面中处理css in js时，往往是将样式加入到元素的style属性中，会大量增加元素的内联样式，并且可能会有大量重复，不易阅读最终的页面代码

### css.module
> 通过命名规范来限制类名太过死板，而css in js虽然足够灵活，但是书写不便。
> css module 开辟一种全新的思路来解决类名冲突的问题

- 思路   css module 遵循以下思路解决类名冲突问题：
                        1. css的类名冲突往往发生在大型项目中
                        2. 大型项目往往会使用构建工具（webpack等）搭建工程
                        3. 构建工具允许将css样式切分为更加精细的模块
                        4. 同JS的变量一样，每个css模块文件中难以出现冲突的类名，冲突的类名往往发生在不同的css模块文件中
                        5. 只需要保证构建工具在合并样式代码后不会出现类名冲突即可

- 实现原理
在webpack中，作为处理css的css-loader，它实现了css module的思想，要启用css module，需要将css-loader的配置```modules```设置为```true```。

原理极其简单，开启了css module后，css-loader会将样式中的类名进行转换，转换为一个唯一的hash值。
由于hash值是根据模块路径和类名生成的，因此，不同的css模块，哪怕具有相同的类名，转换后的hash值也不一样。
- 如何应用样式
css module带来了一个新的问题：源代码的类名和最终生成的类名是不一样的，而开发者只知道自己写的源代码中的类名，并不知道最终的类名是什么，那如何应用类名到元素上呢？
为了解决这个问题，css-loader会导出原类名和最终类名的对应关系，该关系是通过一个对象描述的
这样一来，我们就可以在js代码中获取到css模块导出的结果，从而应用类名了
style-loader为了我们更加方便的应用类名，会去除掉其他信息，仅暴露对应关系
- 其他操作
     1. 全局类名
            某些类名是全局的、静态的，不需要进行转换，仅需要在类名位置使用一个特殊的语法即可：

            ```css
            :global(.main){
                ...
            }
            ```

        使用了global的类名不会进行转换，相反的，没有使用global的类名，表示默认使用了local

            ```css
            :local(.main){
                ...
            }
            ```
        使用了local的类名表示局部类名，是可能会造成冲突的类名，会被css module进行转换

    2. 如何控制最终的类名
            绝大部分情况下，我们都不需要控制最终的类名，因为控制它没有任何意义
            如果一定要控制最终的类名，需要配置css-loader的```localIdentName```

- 其他注意事项
            - css module往往配合构建工具使用
            - css module仅处理顶级类名，尽量不要书写嵌套的类名，也没有这个必要
            - css module仅处理类名，不处理其他选择器
            - css module还会处理id选择器，不过任何时候都没有使用id选择器的理由
            - 使用了css module后，只要能做到让类名望文知意即可，不需要遵守其他任何的命名规范

## PostCss  PostCss类似于一个编译器，可以将样式源码编译成最终的CSS代码
但PostCss和LESS、SASS的思路不同，它其实只做一些代码分析之类的事情，将分析的结果交给插件，具体的代码转换操作是插件去完成的。
这一点有点像webpack，webpack本身仅做依赖分析、抽象语法树分析，其他的操作是靠插件和加载器完成的。
官网地址：https://postcss.org/
github地址：https://github.com/postcss/postcss

- 安装
PostCss是基于node编写的，因此可以使用npm安装
npm i -D postcss
postcss库提供了对应的js api用于转换代码，如果你想使用postcss的一些高级功能，或者想开发postcss插件，就要api使用postcss，api的文档地址是：http://api.postcss.org/

不过绝大部分时候，我们都是使用者，并不希望使用代码的方式来使用PostCss
因此，我们可以再安装一个postcss-cli，通过命令行来完成编译
npm i -D postcss-cli
postcss-cli提供一个命令，它调用postcss中的api来完成编译

- 命令的使用方式为：
postcss 源码文件 -o 输出文件
配置文件
和webpack类似，postcss有自己的配置文件，该配置文件会影响postcss的某些编译行为。
配置文件的默认名称是：postcss.config.js

例如：
module.exports = {
    map: false, //关闭source-map
}
插件
光使用postcss是没有多少意义的，要让它真正的发挥作用，需要插件

postcss的插件市场：https://www.postcss.parts/

- 下面罗列一些postcss的常用插件
        1.postcss-preset-env  它称之为postcss预设环境，大意就是它整合了很多的常用插件到一起，并帮你完成了基本的配置，你只需要安装它一个插件，就相当于安装了很多插件了。   ：
                        1.自动的厂商前缀  某些新的css样式需要在旧版本浏览器中使用厂商前缀方可实现     
                        2.未来的CSS语法 
                                CSS的某些前沿语法正在制定过程中，没有形成真正的标准，如果希望使用这部分语法，为了浏览器兼容性，需要进行编译
                                过去，完成该语法编译的是cssnext库，不过有了postcss-preset-env后，它自动包含了该功能。
                                你可以通过postcss-preset-env的stage配置，告知postcss-preset-env需要对哪个阶段的css语法进行兼容处理，它的默认值为2
                        3.变量  未来的css语法是天然支持变量的
                        4.自定义选择器
        2.postcss-apply  该插件可以支持在css中书写属性集  类似于LESS中的混入，可以利用CSS的新语法定义一个CSS代码片段，然后在需要的时候应用它
        3.postcss-color-function  该插件支持在源码中使用一些颜色函数
    
        4.stylelint
                    官网：https://stylelint.io/

                    在实际的开发中，我们可能会错误的或不规范的书写一些css代码，stylelint插件会即时的发现错误

                    由于不同的公司可能使用不同的CSS书写规范，stylelint为了保持灵活，它本身并没有提供具体的规则验证

                    你需要安装或自行编写规则验证方案

                    通常，我们会安装stylelint-config-standard库来提供标准的CSS规则判定

                    安装好后，我们需要告诉stylelint使用该库来进行规则验证

                    告知的方式有多种，比较常见的是使用文件.stylelintrc

                    //.styleintrc
                    {
                    "extends": "stylelint-config-standard"
                    }
                    此时，如果你的代码出现不规范的地方，编译时将会报出错误
### 在webpack中使用

## 抽离css文件
目前，css代码被css-loader转换后，交给的是style-loader进行处理。

style-loader使用的方式是用一段js代码，将样式加入到style元素中。

而实际的开发中，我们往往希望依赖的样式最终形成一个css文件

此时，就需要用到一个库：`mini-css-extract-plugin`

该库提供了1个plugin和1个loader

- plugin：负责生成css文件
- loader：负责记录要生成的css文件的内容，同时导出开启css-module后的样式对象

使用方式：
const MiniCssExtractPlugin = require("mini-css-extract-plugin")
module.exports = {
    module: {
        rules: [
            {
                test: /\.css$/, use: [MiniCssExtractPlugin.loader, "css-loader?modules"]

            }
        ]
    },
    plugins: [
        new MiniCssExtractPlugin({
            filename: "css/[name].[contenthash:5].css"
        })
    ]
}


# 关于js的兼容性问题  




## babel的出现，就是用于解决这样的问题，它是一个编译器，可以把不同标准书写的语言，编译为统一的、能被各种浏览器识别的语言


- babel的安装
babel可以和构建工具联合使用，也可以独立使用
        如果要独立的使用babel，需要安装下面两个库：
        @babel/core：babel核心库，提供了编译所需的所有api
        @babel/cli：提供一个命令行工具，调用核心库的api完成编译
                    npm i -D @babel/core @babel/cli
- babel的使用
@babel/cli的使用极其简单
它提供了一个命令babel
                    - 按文件编译
                    babel 要编译的文件 -o 编辑结果文件

                    - 按目录编译
                    babel 要编译的整个目录 -d 编译结果放置的目录
- babel的配置
可以看到，babel本身没有做任何事情，真正的编译要依托于babel插件和babel预设来完成
babel预设和postcss预设含义一样，是多个插件的集合体，用于解决一系列常见的兼容问题
如何告诉babel要使用哪些插件或预设呢？需要通过一个配置文件.babelrc

                {
                    "presets": [],
                    "plugins": []
                }

### babel的预设  设定兼容范围


### babel的插件
        通常情况下，@babel/preset-env只转换那些已经形成正式标准的语法，对于某些处于早期阶段、还没有确定的语法不做转换。
        如果要转换这些语法，就要单独使用插件
### 在webpack中使用 bable
下载 npm i -D @babel/core babel-loader @babel/preset-env   
webpack中配置规则
module{reles[{test:/\.js$/,use:"babel-koader"}]  把js文件全部交给babel-koader}

写一个.babelrc 文件进行配置
{
    "presets":[
        [
            "@babel/preset",{
                "useBuiltins":"usage",
                "corejs":3
            }
        ]
    ]
}
注意如果使用了新的语法 还需要额外下载其他库来支持  比如promise



# 性能优化
本章所讲的性能优化主要体现在三个方面：
## **构建性能**
        这里所说的构建性能，是指在**开发阶段的构建性能**，而不是生产环境的构建性能优化的目标，**是降低从打包开始，到代码效果呈现所经过的时间**构建性能会影响开发效率。构建性能越高，开发过程中时间的浪费越少
### 减少模板解析
模块解析包括：抽象语法树分析、依赖分析、模块语法替换
如果某个模块不做解析，该模块经过loader处理后的代码就是最终代码。
如果没有loader对该模块进行处理，该模块的源码就是最终打包结果的代码。
如果不对某个模块进行解析，可以缩短构建时间
- 哪些模块不需要解析？
模块中无其他依赖：一些已经打包好的第三方库，比如jquery
- 如何让某个模块不要解析？
配置`module.noParse`，它是一个正则，被正则匹配到的模块不会解析
### 优化loader性能  进一步限制loader的应用范围
思路是：对于某些库，不使用loader   例如：babel-loader可以转换ES6或更高版本的语法，可是有些库本身就是用ES5语法书写的，不需要转换，使用babel-loader反而会浪费构建时间
lodash就是这样的一个库
> lodash是在ES5之前出现的库，使用的是ES3语法
通过`module.rule.exclude`或`module.rule.include`，排除或仅包含需要应用loader的场景

我们可以基于一种假设：如果某个文件内容不变，经过相同的loader解析后，解析后的结果也不变
于是，可以将loader的解析结果保存下来，让后续的解析直接使用保存的结果
`cache-loader`可以实现这样的功能  `cache-loader`还可以实现各自自定义的配置，具体方式见文档

`thread-loader`会开启一个线程池，线程池中包含适量的线程
### 热替换  
 热替换并不能降低构建时间（可能还会稍微增加），但可以降低代码改动到效果呈现的时间


## **传输性能**
传输性能是指，打包后的JS代码传输到浏览器经过的时间 在优化传输性能时要考虑到：
                    1. 总传输量：所有需要传输的JS文件的内容加起来，就是总传输量，重复代码越少，总传输量越少
                    2. 文件数量：当访问页面时，需要传输的JS文件数量，文件数量越多，http请求越多，响应速度越慢
                    3. 浏览器缓存：JS文件会被浏览器缓存，被缓存的文件不会再进行传输
### 分包
#### 手动分包



**手动打包的过程**：

            1. 开启`output.library`暴露公共模块
            2. 用`DllPlugin`创建资源清单
            3. 用`DllReferencePlugin`使用资源清单

            **手动打包的注意事项**：
            1. 资源清单不参与运行，可以不放到打包目录中
            2. 记得手动引入公共JS，以及避免被删除
            3. 不要对小型的公共JS库使用

            **优点**：
            1. 极大提升自身模块的打包速度
            2. 极大的缩小了自身文件体积
            3. 有利于浏览器缓存第三方库的公共代码

            **缺点**：
            1. 使用非常繁琐
            2. 如果第三方库中包含重复代码，则效果不太理想

#### 自动分包
- 原理
自动分包的原理其实并不复杂，主要经过以下步骤：

1. 检查每个chunk编译的结果
2. 根据分包策略，找到那些满足策略的模块
3. 根据分包策略，生成新的chunk打包这些模块（代码有所变化）
4. 把打包出去的模块从原始包中移除，并修正原始包代码

在代码层面，有以下变动
1. 分包的代码中，加入一个全局变量，类型为数组，其中包含公共模块的代码
2. 原始包的代码中，使用数组中的公共代码

### 代码压缩
1. **为什么要进行代码压缩**
减少代码体积；破坏代码的可读性，提升破解成本；
2. **什么时候要进行代码压缩**
生产环境
3. **使用什么压缩工具**
目前最流行的代码压缩工具主要有两个：`UglifyJs`和`Terser`
`UglifyJs`是一个传统的代码压缩工具，已存在多年，曾经是前端应用的必备工具，但由于它不支持`ES6`语法，所以目前的流行度已有所下降。
`Terser`是一个新起的代码压缩工具，支持`ES6+`语法，因此被很多构建工具内置使用。`webpack`安装后会内置`Terser`，当启用生产环境后即可用其进行代码压缩。
因此，我们选择`Terser`
**关于副作用 side effect**

副作用：函数运行过程中，可能会对外部环境造成影响的功能
如果函数中包含以下代码，该函数叫做副作用函数:
        - 异步代码
        - localStorage
        - 对外部数据的修改
如果一个函数没有副作用，同时，函数的返回结果仅依赖参数，则该函数叫做纯函数(pure function)

- Terser

在`Terser`的官网可尝试它的压缩效果
> Terser官网：https://terser.org/
- webpack+Terser
webpack自动集成了Terser
如果你想更改、添加压缩工具，又或者是想对Terser进行配置，使用下面的webpack配置即可
```js
const TerserPlugin = require('terser-webpack-plugin');
const OptimizeCSSAssetsPlugin = require('optimize-css-assets-webpack-plugin');
module.exports = {
  optimization: {
    // 是否要启用压缩，默认情况下，生产环境会自动开启
    minimize: true, 
    minimizer: [ // 压缩时使用的插件，可以有多个
      new TerserPlugin(), 
      new OptimizeCSSAssetsPlugin()
    ],
  },
};
```


### tree shaking
> 压缩可以移除模块内部的无效代码
> tree shaking 可以移除模块之间的无效代码
### 懒加载

## 其他优化 
### ESlint
ESLint是一个针对JS的代码风格**检查**工具，当不满足其要求的风格时，会给予警告或错误
官网：https://eslint.org/
民间中文网：https://eslint.bootcss.com/

- 使用
ESLint通常配合编辑器使用
1. 在vscode中安装`ESLint`

### bundle analyzer 分析性能原因

### gzip

gzip是一种压缩文件的算法
-  B/S结构中的压缩传输

-  使用webpack进行预压缩
使用`compression-webpack-plugin`插件对打包结果进行预压缩，可以移除服务器的压缩时间




## **运行性能**
运行性能是指，JS代码在浏览器端的运行速度 它主要取决于我们如何书写高性能的代码
**永远不要过早的关注于性能**，因为你在开发的时候，无法完全预知最终的运行性能，过早的关注性能会极大的降低开发效率

性能优化主要从上面三个维度入手   **性能优化没有完美的解决方案，需要具体情况具体分析**


# 
html css js 文件压缩
https://blog.csdn.net/Michael_lcf/article/details/92797843


# 搭建多页应用
https://github.com/yjisme/multi-static-pages-webpackproj