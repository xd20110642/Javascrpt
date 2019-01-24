##vue-cli 


##在index.html页面里添加 媒体查询内容
	 <meta name="viewport" content="width=device-width,initial-scale=1.0,maximum-scale=1.0,minimum-scale=1.0,user-scalable=no">
##在组件中定义传递过来的props的类型

	`props:{
	a:{
	type:Object
	}
	}
	`

##可以在组件外包裹一层div然后来控制样式

##减小打包体积和使用新语法的api 
	参考链接<a>http://www.mamicode.com/info-detail-2289719.html</a>
1. 安装babel-runtime和babel-polyfill插件
		
		npm i babel-runtime babel-polyfill --save-dev
2.	注意：使用babel-polyfill 需要将其放在main.js的第一行 否者将不会被执行
3.	而babel-rutime 需要将其添加在.barle配置文件中

##解决移动端点击事件问题
	参考链接<a>https://blog.csdn.net/zfy865628361/article/details/49512095</a>
1.安装fastclick插件 
		
		npm i fastclick --save-dev
2. 也是需要在main.js中引入	
			
			import fastclick from 'fastclick'//引入
			fastclick.attach(document.body)//实例化


##jsonp跨域 
1.安装jsonp 
	
	npm i jsonp

2.封装jsonp
		
		import originJSONP from 'jsonp';

		/** * 封装jsonp
		 *  @param {*} url 原始的jsonp第一个参数是url，第二个参数是option，这里为了比较好写参数做了下封装
		 *  @param {obj} data 参数
		 * @param {*} option jsonp的option
		 */
		export default function jsonp(url,data,option){
		    url+=(url.indexOf('?')<0?'?':'&')+param(data);
		    return new Promise((resolve,reject) => {
		        //  这里是jsonp自带的数据格式
		        /**
		         * callback ===> (err,data)
		         * (url,opts,callback)  ====  (url,opts,(err,data))
		         * 
		         */
		        originJSONP(url,option,(err,data) => {
		            // 没有错->就返回正确的数据
		            if(!err){
		                resolve(data)
		            }else{
		                reject(err)
		            }
		        })
		    })
		}
		function param(data){
		    let url='';
		    for(var k in data){//遍历对象
		        // 如果value等于undefined 那么就返回 ''
		        let value=data[k] !=undefined?data[k]:'';
		        // encodeURIComponent进行编码
		        url+=`&${k}=${encodeURIComponent(value)}`
		    }
		    return url?url.substring(1):'';
		}

##使用iviewui的轮播图 
1.需要在img里面设置一个class样式，然后设置宽高 然后就可以适应 我们定义的大小了



##使用keep-alive 能在组件切换过程中将状态保留在内存中，防止重复渲染DOM
1.使用方法
		
		<keep-alive>
			<router-view></router-view>
		</keep-alive>


##使用字符串
1. :a=" '这样就是字符' "



##使用refs的知识点
1.使用在组件上面
	
		　<information ref='information'></information>
		　this.$refs.information.isAdd;  
		　
		　
2.使用在元素上面
		
			<span ref="myspan" class="redmy">23232</span>
			this.$refs["myspan"].className  //redmy
			this.$refs["myspan"]   指代对象//<span class="redmy">23232</span>		　		　		　
			
##在数据初始化时操作DOM和在加载完成DOM时 操作DOM

是回调的 this 自动绑定到调用它的实例上

Vue.nextTick(callback)，当数据发生变化，更新后执行回调。
	
	这个是在初始化数据的时候使用，也就是在create生命周期使用

Vue.$nextTick(callback)，当dom发生变化，更新后执行的回调。
	
	这个是在DOM已经被渲染完的时候使用,也就是在mounted生命周期使用			
##使用vue-awesome-swiper插件的问题
 引起轮播异常的常见问题
 https://blog.csdn.net/m0_37885651/article/details/81084681
 
 https://blog.csdn.net/Fancy_Q/article/details/81975516		