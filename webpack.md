title: webpack
speaker: fy.li
plugins:
    - echarts

<slide  class="bg-black aligncenter" image="https://source.unsplash.com/random .dark">

## 初学 [webpack](https://webpack.docschina.org/) {.text-landing.text-shadow}
---
By fy.li {.text-intro}

<slide class="bg-black aligncenter" :class="size-60" image="https://source.unsplash.com/n9WPPWiPPJw/ .anim">
本质上，webpack 是一个用于现代 JavaScript 应用程序的静态模块打包工具。当 webpack 处理应用程序时，它会在内部构建一个依赖图(dependency graph)，此依赖图对应映射到项目所需的每个模块，并生成一个或多个 bundle {.animated.fadeInUp}

<slide  class="bg-black aligncenter" image="https://source.unsplash.com/random .dark">

- [entry](http://192.168.5.153:8080/#slide=4)(入口) {:&.bounceIn}
- output(输出) {:&.bounceIn}
- loader(转换器) {:&.bounceIn}
- plugin(插件) {:&.bounceIn}
- mode(模式) {:&.bounceIn}

<slide :class="size-50 aligncenter">
### entry

###### 入口起点(entry point)指示 webpack 应该使用哪个模块，来作为构建其内部 依赖图(dependency graph) 的开始。进入入口起点后，webpack 会找出有哪些模块和库是入口起点（直接和间接）依赖的。
---
```shell {.animated.fadeInUp}
    entry: './src/index.js', //指定构建入口
    entry: ['./src/index.js', '.src/foo.js'], //指定构建入口
    entry: {
        main: './src/index.js',
        foo: './src/foo.js',
    },
```

<slide :class="size-50 aligncenter">

### output

##### output属性告诉 webpack 在哪里输出它所创建的 bundle，以及如何命名这些文件。
---
```shell {.animated.fadeInUp}
  module.exports = {
  output: {
    path: path.resolve(__dirname, 'dist'),
    filename: 'my-first-webpack.bundle.js'
  }
};
```
<slide :class="size-50 aligncenter">

### loader

##### webpack 只能理解 JavaScript 和 JSON 文件，这是 webpack 开箱可用的自带能力。loader 让 webpack 能够去处理其他类型的文件，并将它们转换为有效 模块，以供应用程序使用，以及被添加到依赖图中。
---
```shell {.animated.fadeInUp}
  module.exports = {
        rules: [
            {
                test: /\.css$/i,
                use: [
                    MiniCssExtractPlugin.loader,
                    'css-loader'
                ]
            },
            {
                test: /\.scss$/,
                use: ['style-loader', 'css-loader', 'sass-loader']
            },
            {
                test: /\.(png|jpg|gif)$/i,
                use: [{
                    loader: 'url-loader',
                    options: {
                        // name: '[name].[ext]'
                        limit: 8192
                    }
                }]
            }
        ]
};
```


<slide :class="size-50 aligncenter">
### plugin

##### loader 用于转换某些类型的模块，而插件则可以用于执行范围更广的任务。包括：打包优化，资源管理，注入环境变量
---
```shell {.animated.fadeInUp}
  module.exports = {
    plugins: [
        new MiniCssExtractPlugin({
            filename: '[hash].css',
        }),
        new HtmlWebpackPlugin({
            template: 'src/index.html', // 配置默认模板文件
        }),
        // new BundleAnalyzerPlugin(), // 
        new webpack.HotModuleReplacementPlugin(),
        new webpack.NamedModulesPlugin()
    ],
};
```


<slide :class="size-50 aligncenter">

### mode

#####  通过选择 development, production 或 none 之中的一个，来设置 mode 参数，你可以启用 webpack 内置在相应环境下的优化。其默认值为 production

<slide class="bg-apple aligncenter">
![](./static/image1.jpg)
:::
<slide class="bg-apple aligncenter">
![](./static/menu.jpg)
:::


<slide :class="size-50">

##  :fa-heart-o: Loader


* :raw-loader\::{.text-intro}  加载文件内容
* :file-loader\::{.text-intro} 图片加载，生成file文件，输出到指定目录并返回url
* :url-loader\::{.text-intro} 基本与file-loader相似，可以设置一个limit值，小于这个值的可以打包成base64位的文件
* :css-loader\::{.text-intro} 加载 CSS，支持模块化、压缩、文件导入等特性
* :style-loader\::{.text-intro} 把CSS代码注入到JavaScript中，通过DOM加载CSS
* :sass-loader\::{.text-intro}  将scss/sass转换为css
* :babel-loader\::{.text-intro}  将ES6转换为ES5
{.description}


<slide :class="size-50">

##  :fa-heart-o: plugin


* :MiniCssExtractPlugin\::{.text-intro}  将css文件单独打包成一个文件
* :HtmlWebpackPlugin\::{.text-intro} 简单创建 HTML 文件，用于服务器访问
* :HotModuleReplacementPlugin\::{.text-intro} 启用模块热替换(Enable Hot Module Replacement - HMR)
* :DllPlugin\::{.text-intro} 为了极大减少构建时间，进行分离打包
* :DllReferencePlugin\::{.text-intro} 这个插件是在 webpack 主配置文件中设置的， 这个插件把只有 dll 的 bundle(们)(dll-only-bundle(s)) 引用到需要的预编译的依赖。
* :BundleAnalyzerPlugin\::{.text-intro} 分析打包后bundle的大小
{.description}

<slide class="bg-apple aligncenter">
![](./static/image1.jpg)
:::

<slide :class="size-50">

##### Webpack 的运行流程是一个串行的过程，从启动到结束会依次执行以下流程：
---

* 初始化参数：从配置文件和 Shell 语句中读取与合并参数，得出最终的参数( 这个过程中还会执行配置文件中的插件实例化语句 new Plugin())
* 开始编译：用上一步得到的参数初始化 Compiler 对象，加载所有配置的插件，执行对象的 run 方法开始执行编译
* 确定入口：根据配置中的 entry 找出所有的入口文件
* 编译模块：从入口文件出发，调用所有配置的 Loader 对模块进行翻译，再找出该模块依赖的模块，再递归本步骤直到所有入口依赖的文件都经过了本步骤的处理
* 完成模块编译：在经过第4步使用 Loader 翻译完所有模块后，得到了每个模块被翻译后的最终内容以及它们之间的依赖关系
* 输出资源：根据入口和模块之间的依赖关系，组装成一个个包含多个模块的 Chunk，再把每个 Chunk 转换成一个单独的文件加入到输出列表，这步是可以修改输出内容的最后机会
* 输出完成：在确定好输出内容后，根据配置确定输出的路径和文件名，把文件内容写入到文件系统
---
在以上过程中，Webpack 会在特定的时间点广播出特定的事件，插件在监听到感兴趣的事件后会执行特定的逻辑，并且插件可以调用 Webpack 提供的 API 改变 Webpack 的运行结果。


<slide class="bg-apple aligncenter">
![](./static/image2.jpg)

<slide class="fullscreen bg-blue" youtube=".dark id='KbNL9ZyB49c' autoplay loop" :class="aligncenter">

## **编写一个[loader](https://www.webpackjs.com/contribute/writing-a-loader/)和[plugin](https://www.webpackjs.com/contribute/writing-a-plugin/)**

<slide :class="size-50">

## Compiler 和 Compilation

在开发 Plugin 时最常用的两个对象就是 Compiler 和 Compilation，它们是 Plugin 和 Webpack 之间的桥梁。 Compiler 和 Compilation 的含义如下：

* Compiler 对象包含了 Webpack 环境所有的的配置信息，包含 options，loaders，plugins 这些信息，这个对象在 Webpack 启动时候被实例化，它是全局唯一的，可以简单地把它理解为 Webpack 实例；
* Compilation 对象包含了当前的模块资源、编译生成资源、变化的文件等。当 Webpack 以开发模式运行时，每当检测到一个文件变化，一次新的 Compilation 将被创建。Compilation 对象也提供了很多事件回调供插件做扩展。通过 Compilation 也能读取到 Compiler 对象

Compiler 和 Compilation 的区别在于：Compiler 代表了整个 Webpack 从启动到关闭的生命周期，而 Compilation 只是代表了一次新的编译。
<!-- <slide youtube=".dark id='_m67JbGjWnc' autoplay loop"> -->

<slide class="bg-black-blue aligncenter" image="https://i.loli.net/2020/10/19/LxuGP9wqhTMyFBZ.jpg bg-black-blue" >  
## **荣耀剑下取，均衡乱中求**