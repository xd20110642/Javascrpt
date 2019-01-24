#再次学习Vue
##不使用构建版本,使用网页版本
1.在实例化的时候，是大写的 Vue
	
	响应式的数据
		
		var data = {
   			 a: 1
			}
			var vm = new Vue({
			    el: '#app',
			    data: data
			})
		data.b=1;//这个就不是响应式的了 因为实例化后才注入的
		
	现在data里面的a才是响应式的，因为他是在实例化前 就应经是被注入了,对b的改动不会触发视图的任何改动
	**可以使用修改 但是这个地方稍后补偿**
	主要是针对数组和对象来说   通过下标来修改vue不能监听到 
	
	arr:[1,2,3]
	arr[0]=a =>vue监听不生效
	vue.set(arr,0,a) => 生效	
	
	使用Vue.set(object,key,value) <===>vm.set(object,key,value)
	这样就可以将其修改为响应式数据
	vm.$set(vm.data,'age',26) ===> data{a:1,age:26}
实例会暴露出以$开头的方法

 	例如：vm.$data ===data  
 	vm.$el===document.getElementById('app');
 	
生命周期钩子（最常用）：

	created(){//初始化数据的生命周期钩子
	
	} 	
	mounted(){//DOM加载完毕的时候，使用操作DOM
	
	}
2 模板语法

	v-bind:href='xxx' --> 绑定样式 缩写 --->  :href='xxx'
	
	v-on:click='one' ----> 绑定事件  缩写 --> @click='xxxx'
	
3 计算属性和侦听属性
	
		计算属性定义的变量，可以不需要在data中定义  他是有缓存的 都需要有缓存机制
		computed:{
			xxx(){
			return xxx
			}
		}
		
		侦听属性是需要现在data里面定义的
		watch:{
			question(new,old){
				//new 是状态
				//old 是旧状态
			}
		}
		
		
4 class和style绑定
	
	使用v-bind来绑定class和style  可以是单个字符串、数组、对象
	
4.1	对象语法
		
		<div :class="{active:isActive}"></div>
active这个class的是否存在 取决于date中的isActive的是否存在

		<div :class="classObject></div>	
		
		data:{
		classObject:{
			active:true
		}
		}
5 条件渲染

 5.1 用key来做唯一标识		
 5.2使用v-for把一个(数组、对象)对应为一组元素
 	
 		<li v-for="(item,key) in items" :key="index">
 			{{item.mess}}
 		</li>		
			
5.2.1使用v-for来渲染 <tenplate>模板
	
	<ul>
	  <template v-for="item in items">
	    <li>{{ item.msg }}</li>
	    <li class="divider" role="presentation"></li>
	  </template>
	</ul>
			
6.事件处理
	
	一般不带括号
7.表单输入绑定

1. 需要使用v-model 来完成双向数据绑定	
2. 多选框的使用方法
	
		  <select v-model="selected">
            <option disabled value="">请选择</option>
            <option>A</option>
            <option>B</option>
            <option>C</option>
        </select>
3. 修饰符 .lazy
	
		将input事件转化为Chage事件进行同步
		v-model.lazy="a"
8.组件基础
	1.	定义一个组件	并且是全局组件	       
	Vue.component('组件名称',{
		template:'#app',//这个地方可以使用template来完成
		data(){
		return {
		
		}
		}
	})
		
	<template id="app">
	//就和组件里面的内容对应起来了
	
	</template>	
		2.通过prop向子组件传递数据 
		
		通过属性绑定的方法来完成数据的传递
		<xd :name="xxxx"></xd>
		组件接受
		props:['name']
	3.通过事件监听来完成 子组件对父组件的完成	
		<xd @click="a"></xd>	
		子组件通过：this.$emit('xx')来完成触发
**最优的解决方法 是使用vuex**		
	4.插槽
		如果在组件中间需要自定义内容例如
		
		<template>
			<div>
				<p>xxx</p>
			</div>
		</template>
		
		<xd>xxxxx</xd>  ===> 会报错
		
		但是如果在模板中加入插槽<solt></solt>那么就不会报错
		
		<template>
			<div>
				<p>xxx</p>
				<solt></solt>
			</div>
		</template>
		
			<xd>xxxxx</xd>  ===> 不会报错

9 prop

1. 可以初始化定义传入的props的类型和初始化值


				props:{
				title:String,
				likes:{
					type：Number,
					default:1
				},
				arr:{//定义数组和对象的默认值，必须从一个工厂函数获取
				type:object,
				default(){
				return {mess:'hello}
				},
				func:{//自定义验证函数
				validator(value){
				// 这个值必须匹配下列字符串中的一个
		      return ['success', 'warning','danger'].indexOf(value) !== -1		}
				}
				}
				}
2. 使用props:['a'],中的数据是使用**this.a来完成使用**

9 插槽

1.使用普通插槽

在组件的内部直接使用

	<template id="hear">
            <div style="width:100%;height:200px;background:pink">
            我是头部组件
            <slot></slot>
        </div>
    </template>
    
    <hear>我是使用了普通插槽的方法了</hear>
 2.使用具名插槽
 	
 	
 	组件
 	<hear>
 		  <template slot="foo">
                <h1>Here might be a page title</h1>
            </template>
 	</hear>
 	   
		<template id="hear">
            <div>
                <slot name="foo"></slot>
      		  </div>
    </template>	
    
指定渲染 具名插槽需要使用 templte 来完成

10 动态组件和异步组件

1. 使用keep-alive来完成对组件的缓存，避免组件重复渲染,使用is来切换不同的组件

	<keep-live>
		<hear></hear>
	</keep-live>
	
11访问元素&组件

1. 通过DOM直接访问组件

	<div ref="aaa"></div>
	
	this.$refs.aaa

12 过渡效果

13 使用插件

1. 通过全局方法使用插件
	
	Vue.use() //需要在new Vue实例化前 完成
	<!--也可以传递一个选项对象-->
	Vue.use(xxx,{aaa:true})			
14 过滤器

1. 在{{mess|xxx}} //在花括号中
2. 在 <div v-bind:id="rawId|xxx"></div>	
3. 定义全局过滤器
		
		Vue.filter('过滤器名字',function(value){//value就是我们|前面的内容
		if(!value){
			return ''
		}
		value=value.toString()
		return xxxx;
		
		})
			
15 混入属性
	
	执行顺序:混入先执行,原生的后执行 注意：不是覆盖而是分别执行一次
	
	1. 定义混入对象 我们可以再混入对象里面使用完整的vue的所有方法和事件
	//定义混入对象
		var myminxin={
			created(){
				this.hello //这个this指向我们混入的vue对象实例
			}
		}
	2. 实例化
	var vm=new Vue({
		mixins:[我们定义的混入对象的名字]
	})	

16 动态组件 使用 component 组件来完成对组件的动态显示

	根据is 来动态切换组件
	
	<component :is="componentId"></component>				