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
<slide class="bg-black" :class=" size-40 aligncenter" image="https://cn.bing.com/az/hprichbg/rb/WinterLynx_ZH-CN7158207296_1920x1080.jpg .dark">
