#webpack学习
1.	在package.json文件中的配置写法

		 "scripts": {
	    "build": "webpack" //这个是打包成生产环境的 后面可以跟上参数
	    "dev":"webpack-dev-server" //这个是将其打包在内存中 也就是 在开发环境中使用的   后面也是可以更上参数的
	   
	 	 },
2. 加载相对应的模块
	1. 解决css模块 需要安装 css-loader style-loader 
	2. 解决图片的引入 需要安装 file-loader url-loader 
	
	
	
	
	
	2. 然后在配置文件中建立模块然后在模块中，使用正则来匹配规则
	
			module:{
				//匹配规则
				rules:[ 
					{
					test:/\.css$/  //匹配所有的.css后缀
					use:[//使用到的模块
						'style-loader',
						'css-loader'
					]
					},
					{
						test:/\.(png|svg)$/,
						use:[
							{
                        loader: 'url-loader',
                        options: {
                            limit: 8192,    // 小于8k的图片					自动转成base64格式，并且不会存在实体图片
                            outputPath: 'images/'   // 图片				打包后存放的目录
                        }
                    }
						]
					
					}
				]
			}	
	
3. 使用插件
	1. 使用页面打包插件动态生成一个页面,依赖html-webpack-plugin
	
	
	2. 使用插件
		const Html=require('xxx')
		plugins:[
			new Html({
			temlpalce:'' //模板
			hash:true //// 会在打包好的bundle.js后面加上hash串
			})
		]
	
		 	 
2. webpack.config.js配置文件
	
		
		const path=require('path');
		
		module.exports={
		
		entry:"",//唯一入口文件
		output:{ //输入文件配置
		filename:""//输出文件的名字 [name]可以和上面的入口文件保持一致	
		path:path.resolve(__dirname,'dist')//输出的路径
		},
		module:{
			//匹配规则
			rules:[ 
			test:/\.css$/  //匹配所有的.css后缀
			use:[//使用到的模块
			'style-loader',
			'css-loader'
					]
				]
		 	}
		}	 	 
		
3. 入口文件的属性和配置

		index.js
		
		import './style.css' //引入css
		

			