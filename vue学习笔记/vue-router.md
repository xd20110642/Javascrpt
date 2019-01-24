#vue路由
---
1.路由守卫
	
	利用路由提供的钩子函数来判断是否需要登陆验证
	router.beforeEach((to, from, next) => {
  		if(to.meta.xx){
			next();
		}else{
			next({
                path: '/login',
                query: {redirect: to.fullPath}  // 将跳转的路由path作为参数，登录成功后跳转到该路由
            })
		}else{
		next()	
	})



	to: Route: 即将要进入的目标 路由对象
	from: Route: 当前导航正要离开的路由
	next: Function: 一定要调用该方法来 resolve 这个钩子。执行效果依赖 next 方法的调用参数。
		- next(): 进行管道中的下一个钩子。如果全部钩子执行完了，则导航的状态就是 confirmed （确认的）。
		- next(false): 中断当前的导航。如果浏览器的 URL 改变了（可能是用户手动或者浏览器后退按钮），那么 URL 地址会重置到 from 路由对应的地址。
		- next('/') 或者 next({ path: '/' }): 跳转到一个不同的地址。当前的导航被中断，然后进行一个新的导航。


	**确保要调用 next 方法，否则钩子就不会被 resolved**

	//  if(登录 || to.name === 'login'){ next() } // 登录，或者将要前往login页面的时候，就允许进入路由  这个是一种判断方法




2.vue路由设置meta   路由元信息  一般是用来设置路由守卫检查的 也可以配置其他的内容
其他内容查看 
<a>https://www.cnblogs.com/nns4/p/8589539.html</a>
	
		 meta: { requiresAuth: true } //这个是用于判断是否需要验证用户

获取meta设置的内容，在berforeEach生命周期中 使用

		to.meta.xxxx 来获取参数



#使用keep-alive组件 缓存组件状态 防止多次请求
		
			    <keep-alive> //最常用的方法
       			 <router-view></router-view>
   				</keep-alive>

---
参考链接 <a>https://juejin.im/post/5b41bdef6fb9a04fe63765f1#heading-18</a>