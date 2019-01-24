#mpvue小程序框架
----
##全局函数 也就是app函数 这个对应到的时 App.vue里面的函数

1. created   =====> onLaunch    是一样的可以全局调用一次    全局数据初始化   获取用户信息   created早于 onlaunch 完成
2. onshow方法

		`
		onshow(options){//接受一个参数 可以通过这个参数来获取场景值
			console.log(option)
		}
	`
来判断用户是通过什么渠道进入 我们的小程序的



##page文件夹
1.	并且每一个都是inde.vue  和main.js文件
2. 每一个文件夹下面必须有一个 main.js 用来当配置文件
	3.  `
		import Vue from 'vue'
		import App from './index'
		const app = new Vue(App)
		app.$mount()
		`
                     
##注意事项
1. 只能使用 ` <button open-type="getUserInfo">授权用户信息</button>`  来获取用户信息

##使用ui框架
1. 首先在github上面将框架clone下来
2. 然后将其中的dist目录，放置到mpvue产生的dist目录下。（可将ui框架的dist目录重命名）
3. 然后在页面的package.json文件种加入

		"usingComponents": { 
    	"i-button": "../../dist/button/index" //这里就是我们引入的组件
		}

4.	使用就是即可
	
		<i-button type="primary" bind:click="handleClick">这是一个按钮</i-button>



##爬坑日记
1. 使用微信轮播图组件时，必须将相关的相关信息写在里面组件的上面，不能使用定义在data()里面的变量
2. 不能使用微信官方提供的小程序组件的名字 来令名组件  否则会出错
3. 每添加一个页面，也就是pages  必须重新运行 也就是npm run dev 如果不重新运行 就会报错
4. 在设置tar栏的时候 图片不会被自动引入 需要自己 手动引入，  **并且在配置文件中，不能有空格**
5. 跳转页面是 使用相对路径 也就是 a页面相对于b页面的路径  wx.navigateTo() 不能跳转 tab下面配置的页面
6. 设置不同页面的文字，需要在pages文件下面 添加main.json {xxx:xxx} 就可以了
7. 用户授权获取用户头像 
  
		<button open-type="getUserInfo" @getuserinfo="自定义函数">用户授权</button>
		methods:{
			登陆函数
		}

8.	mpvue里面使用微信官方提供的api 如果有多层嵌套必须使用 只能使用箭头函数 只用 this 否者会报错
	
				success: res =>{ //这样this才能只能指向全局vue  如果是（res） 那么this为null
                        console.log(res);
                        // console.log(this.addBook)
                        if(res.result){
                          console.log(res.result);
                         console.log(this)  //
                        }
                    },
				
9.	使用fly.js请求数据 一定要带上 httP://xxxx 否者会找不到路径	
10.	获取跳转页面的参数 在生命周期函数里面 使用 this.$root.$mp.query.我们需要获取的字段  目前：测试只能在mouth生命周期里面获取
11.	使用跳转页面，  跳转页面必须在app.json文件里面注册 才能使用否则会报错  **切记 只要是在pages文件夹里面新增的页面，都需要在app.json文件里面去注册 否则会报错**	
12.	使用路由插件 跳转 
13.	
		this.$router.psuh('pages/xx/main')		
14.	不要在vue的created生命周期里获取数据,只要小程序开启,整个项目的所有页面里created生命周期里的方法都会执行一遍,所以不要使用这个生命周期,一般可以写在mounted生命周期里,或者原生的onLoad生命周期里
15.	关于使用switch组件的信息-------> 当check触发事件的时候判断是否选中 那么需要传入一个参数
		
			 getPhone(e){
       	 	if(e.target.value){  e.target.value是 true或者是false
			//通过e.target.value来判断是否选中而不是通过原生的 e.detail.value来判断是否是选中
            
       	 		}else{
				}
		}
16.	注意：使用百度地图的api时，ak是字符串
17.	通过组件传递字符串 " 'xxx' " 这样xxx就是字符串 
18.	可以在全局样式里面 给	**page设置样式**   相当于body 
19.	通过计算属性来判断 是否给定样式

		可以通过传入的给组件的内容来判断
		  props:['score','num'],
   		computed:{
        right(){
            if(this.num){
                return true;
            }else{
                return false;
            }
        }
   		 
		:class="{a:right}" //动态判断给定样式
20.	使用vuex的注意事项

		需要将其挂载到main.js中：
		并且添加到 原型链上
		Vue.prototype.$store=store;  这样就不会报错了
		参考链接：https://blog.csdn.net/qq_31393401/article/details/80728523

21.	使用iviewui 微信小程序ui框架的时候注意事项：
		
			需要将其放置到static静态资源 目录下面，才能正确的引入
			然后在配置一个main.json 文件里面使用引入组件即可
	

		







