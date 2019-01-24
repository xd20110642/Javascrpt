##VUeX  只有共享数据才能发到vuex中，私有数据data 父子组件props vuex共有数据 
-------------
## 安装vuex 
1. 通过script 形式安装 是不需要全局注册
2. 通过webpack 安装的 需要使用 vue.use(vuex) 来全局注册


##实例化vuex

 `const store=new Vuex.Store({
	state:{      // === 相当于data
 		}，
	mutations:{  // ====相当于 methods
	},
	getters:{ //=====相当于 计算属性
	}
	})`
	
	mutations里面的方法是用来操作state里面的数据的


##引入我们组件
把 store 对象提供给 “store” 选项，这可以把 store 的实例注入所有的子组件

    `new Vue({
  	el: '#app',
  // router,
  components: { App },
 	 template: '<App/>'，
	store：store //注入全局组件  只要挂在到vm上，久能使用全局属性
	})`

##使用数据
1. 如果想在组件中 访问store 中的数据  只能通过this.$store.state.xxxxxx         // this.$我们定义的vuex的名字.state.变量
2. 如果想改变store中的数据 那么必须使用mutations中的方法来改变
3. mutations中的函数 里面接受多个参数，但是 第一个参数必须是 state  后面的参数是可以自定义的，**最多2个参数**
	**参数可以为数组和对象         参数为对象=>参数1.a   参数为数组 => 参数1[0]**
	`mutations：{
	a(store,参数1){
	//修改数据
	store.a++//这个是修改store中a的属性
	store.a+ +参数1.a
	}
	}`
4.	子组件要调用mutations中的方法，只能使用this.$我们定义的vuex的名字.commit('方法名')
5.	getters计算属性中：     不会修改原数据 
	`a(state){
	return state.a
	}`
	使用this.$store.getters.我们定义函数名



##总结：
1. state中的数据，不能直接修改，如果想要修改，必须通过mutions
2. 如果组件想要直接从state上获取数据，需要 this.$store.state.xx
3. 如果组件 想要修改数据，必须使用mutations提供的方法，通过this.$store.commit('方法名','唯一的一个参数[')
4. 如果是store中state上的数据，再对外提供的时候，需要做一层包装，那么推荐使用getters,如果需要使用getters,则是this.$store.getters.xxx