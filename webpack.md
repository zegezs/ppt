title: webpack
speaker: fy.li
plugins:
    - echarts

<slide  class="bg-black aligncenter" image="https://source.unsplash.com/random .dark">

## 初学 [webpack](https://webpack.docschina.org/) {.text-landing.text-shadow}
---
By fy.li {.text-intro}

<slide class="bg-black aligncenter" image="https://source.unsplash.com/n9WPPWiPPJw/ .anim">
本质上，webpack 是一个用于现代 JavaScript 应用程序的静态模块打包工具。当 webpack 处理应用程序时，它会在内部构建一个 依赖图(dependency graph)，此依赖图对应映射到项目所需的每个模块，并生成一个或多个 bundle {.animated.fadeInUp}

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
![](./static/image2.jpg)

<slide class="fullscreen bg-blue" youtube=".dark id='KbNL9ZyB49c' autoplay loop" :class="aligncenter">

## **编写一个loader**
<!-- <slide youtube=".dark id='_m67JbGjWnc' autoplay loop"> -->