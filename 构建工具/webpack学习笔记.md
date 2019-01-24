**webpackloader常用插件**

----------
图片压缩：
1. image-webpack-loader  图片压缩
2. uglifyjs-webpack-plugin  压缩插件
 

----------
样式模块：

　　(1)css-loader : 解析css文件中代码

　　(2)style-loader : 将css模块作为样式导出到DOM中

　　(3)less-loader : 加载和转义less文件    还依赖less 

　　(4)sass-loader : 加载和转义sass/scss文件   还依赖 node-sass

　　(5)postcss-loader : 使用postcss加载和转义css/sss文件
	**注意如果使用3 4 模块 必须使用 1 2 模块**

----------
脚本转换编译:

　　(1)script-loader : 在全局上下 文中执行一次javascript文件，不需要解析

　　(2)babel-loader : 加载ES6+ 代码后使用Babel转义为ES5后浏览器才能解析

　　(3)typescript-loader : 加载Typescript脚本文件

　　(4)coffee-loader : 加载Coffeescript脚本文件
	
	(5)babel-plugin-transform-remove-strict-mode 移除严格模式 //配置再.babelrc
----------
Files文件

　　　　(1)raw-loader : 加载文件原始内容(utf-8格式)

　　　　(2)url-loader : 多数用于加载图片资源,超过文件大小显示则返回data URL

　　　　(3)file-loader : 将文件发送到输出的文件夹并返回URL(相对路径)   这个是背景图片是使用

　　　　(4)jshint-loader : 检查代码格式错误




----------


##注意：webpack只能打包处理JS文件，无法处理其他的非js文件
如果要处理非js类型文件，我们需要手动安装一些 适合 第三方 loader加载器

## 引入模块
import ***** from **** 是es6中导入模块的方式  js模块使用

const $ =require('jquery')    //是node引入模块 
  
improt ".xx/xx.css" //引入样式表  非js模块使用   以路径形式，去引入node_module中文件，可以直接省略 路径前面的node_modules 这层

##  使用方法
webpack 要打包的文件的路径  打包完毕输出文件的路径 
wepack  执行webpack.config.js   //只输入webpack 

##  webpack本地服务器  webpack-dev-server工具

1.npm i webpack-dev-server -D 安装到pack.json

2.安装完毕后，用法和webpack命令完全一样

3.由于我们时在本地安装的webpack-dev-server,所以无法把他当成脚本运行，只有那些安装到全局-g的工具 才能在终端中正常支持

4.在package.json中来创建一个命令行，来完成执行这个操作

    "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "dev":"webpack-dev-server"
  	}

5.运行 命令  npm run dev  也就是我们自己定义的名字

6.webpack-dev-server 帮我们打包生成的文件，并没有存放到实际的物理磁盘上，而是，直接托管到了电脑的内存中，所以我们在根目录找不到文件，但是和dist 和src平级  **引入内存文件 直接时 /我们打包出来的目录**

	`    <script src="/bundle.js"></script>

7.常用参数 第一种方式

	`webpack-dev-server  --open` //自动打开浏览器
	webpack-dev-server  --port 3000 //修改端口号
	webpack-dev-server	--contentBase 路径（src） //指定根路径
	webpack-dev-server  --hot //热重载 无刷新重载

8.在配置文件里面设置参数  第二种方式

	devServer: { //这个是配置dev-server对象 里面是属性
        open:true,//自动打开浏览器
        prot:3000,//设置启动端口
        contenBase:'src',//指定托管的根目录
        hot:true//启用热更新
    }
如果在这个模式下要启用热更新：需要如下步骤
	
1. 在配置文件里面 引入webpack模块  const webpack=require('webpack')
2. 在配置文件引入插件节点
	`plugins:[
		        new webpack.HotModuleReplacementFlugin()//new 一个热更新模块
	]`

##使用`html-webpack-plugin`插件配置启动页面 在内存中生成html插件
	
1. 安装插件
2. 在配置文件导入插件  const htmlWebpackPlugin=require('html-webpack-plugin')
3. 然后在plugins插件节点 实例化我们导入的插件名字 
4. 自动把js文件加入到页面中去
  
		`new  htmlWbpackPlugin({
		template:path.join(__dirname,'./src/index.html'), //指定 模板页面，将来会根据指定的页面路径，启用生成内存中的页面
	  	 filename:'index.html'//指定生成页面的名称  只能为index.html
		})`


##处理css文件，需要安装 style-loader css-loader
1. 安装模块  style-loader css-loader
2. 在配置文件中新增节点  module，是一个对象  在这个对象上  有一个rules属性，是一个数组，这数组中存放了所有第三方文件的匹配和处理规则
3. test： 匹配文件路径的正则表达式，通常我们都是匹配文件类型后缀    // 备注：**以/\.开头   以$/结尾  ------>   /\.文件类型 $/  多个类型 用 /\.(css|less)/ 来指定      **
4. include： 指定哪些路径下的文件需要经过 loader 处理，node_module不需要处理，性能问题
5. loader： 单个loader可以直接用这个字段，否者可以用use字段，这些loader一般都需要安装依赖 
6. use：指定使用的loader，use字段是一个数组，注意顺序问题，先使用的loader需要排在后面

	`	module: {//这个节点用于配置所有的第三方模块

        rules: [//所有第三方模块规则
            { 
                test:/\.css$/,   //正则
                use:[
                    'style-loader','css-loader'  //使用那个模块
                ]，
				include:[
					path.resolve(__dirname,'文件地址')//
					]
            }
        ]
   		 },
		`


##处理背景图片路径 使用url-loader 模块  依赖一个file-loader模块

默认情况下，webpack无法处理css文件中的url地址，无论是图片还是字体库，只要有url都无法处理

1. 安装url-loader模块  如果带参数 图片超过我们定义的大小 那么就需要安装file-loader 模块
2. 参数 option{ limit: '1024' } //定义图片大小
3. 使用 

	`  {
                test:/\.(jpg|png|gif|jpeg)$/,
                use: [ //配置参数
                    {
                        loader: "url-loader",
                        options: {
                            limit:'2048'//超过这个大小就不转换
                        }
                    }
                ]
            }`
		《===========   等价 =========》  
 			{
			    test: /\.jpeg$/,
			    use: 'url-loader?limit=1024&name=[hash:8]-[name].[ext] //之前是什么名字就叫什么名字.属性也是一样的  name可以修改为[hash:8]保留8位hash 
			}

处理字体文件
	
	`  { //处理字体文件
                test:/\.(ttf|svg|eot|woff|woff2)$/,
                use: "url-loader"
            }`





##babel 语法转换  需要安装
1. 安装模块 babel-loader 和 babel-plugin-transform-runtime 需要安装和引用  babel-core不需要引用
2. 安装 插件   babel-preset-env 和babel-preset-stage-0    //babel-preset-stage-0 这个是否支持es7的第几个版本
3. 在配置文件中配置，注意在配置babel的loader规则的时候，必须把node_modules目录，通过exclude选项把node排除掉 
4. 然后创建一个.babelrc 的配置文件，这个文件是属于JSON格式，
5. 在配置文件中写如下注释

		`{
			"presets":[”env“], //语法
			"plugins":["transform-runtime"]   //插件 名称只看最后 排除babel-plugin
		}
		`
1. 配置文件webpack.config.js
	1.
	test:/\.js$/,
	use:'babel-loader',
	exclude://



 	//所谓的静态属性 就是可以直接通过 类名，直接访问的属性

    //实例属性： 只能通过类的实例 来访问的属性  叫做实例属性

-----> es6类里面的静态语法: 

	`class xxx{
		static info=123;// 如果要获取到这个方法 那么就是 
	}`
	
	xxx.info 注意是我们定义类来获取的  而不是实例化对象来获取的  而且 this指向的类 而不是实例化对象



##设置配置文件
webpack.config.js  该配置文件就是一个js文件 通过node中的模块操作，向外暴露了一个配置对象

	const path=require('path') //自带的路径模块 
    module.exports={
		entry:path.resolve(__dirname,'入口文件的路径'),    			//定义入口文件 是双_ _
		output:{					//输出文件相关配置
			path:path.resolve(__dirname,'输出文件路径')	
			filename:'我们定义的文件名字'				//定义文件名称
			}，
		plugins:[ //只要是插件都是在plugins这个插件数组里面的  然后实例化插件 也就是new 一个插件名字
		
		
		]，
		module: {//这个节点用于配置所有的第三方模块

        rules: [//所有第三方模块规则
            { 
                test:/\.css$/,   //正则
                use:[
                    'style-loader','css-loader'  //使用那个模块
                ]
            }
        ]
   		 	},							
	}




##项目完成以后 使用webpack 命令打包
webpack --config XXX.js //使用另一份配置文件（比如webpack.config2.js）来打包

 webpack --watch //监听变动并自动打包

 webpack -p//压缩混淆脚本，这个非常非常重要！

 webpack -d//生成map映射文件，告知哪些模块被最终打包到哪里了其中的 

webpack --progress //显示进度条

 webpack --color //添加颜色





----------

##webpack 错误信息：
1. You may need an appropriate loader to handle this file type   缺少模块