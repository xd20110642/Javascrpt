#vuex再次学习
1 基本类型

	state 用来数据共享数据存储
	mutation 用来注册改变数据状态
	getters 用来对共享数据进行过滤操作
	action 解决异步改变共享数据
	
2 初始化以及注入实例对象
		
		const store = new Vuex.Store({
	     state:{//这个就相当于是组件里面的data对象
	         count:0,
	     },
	     mutations:{//这个就相当于是组件里面的methods方法
	         increat(state){//这个必须接受一个参数state
	            state.count++
	         }
	     }	
 		})
		
		var vm=new Vue({
		store,//注入实例化  这个是全局注册vuex，也可以不全局注册  然后在我们需要的组件中    impront 即可
		
		})
		//通过 this.$store.
3 使用mutation方法,也就相当于组件的methods方法 **这个是同步修改数据，如果是异步修改数据的话，数据是不会修改的**
	
		导出
		export default{
		obejtc是参数  单一参数就是可以 ，多个参数为对象
			in(state,obejct){
				
			}
		}
		//使用
		this.$store.commie('name'，‘参数’)
		
			
4 使用getter方法,也就是相当于是计算属性 
	
		
		导出
		export default{
			doneTodos（state）{
			return state.xxx.filter( () => {
			
			})
			}
		}	
		
		//使用   doSome不带括号
		 return this.$store.getters.doSome	
5 使用action方法,是异步修改数据   
**异步修改数据流程    action => mutation => state**

	导出
	export default{
	//参数一:context 这个是固定的写法  通过context来访问：mutation getter state中的内容
	//
	doSome(context,参数的参数){
		settimeOut(	()=>{
		//这个是调用的mutation中的方法
		context.commit('方法名',传入对的参数)
		},1000)
	
	}
	}
	
	//使用
	return this.$store.dispatch('定义的名字')