# vue知识点 #

※在一个html页面里面可以声明多个vue实例 但是在每一个实例里面 只能有一个vue实例  <div id="app"></div> <div id="app2"></div>  成立   <div id="app"><div id="app"></div> </div> 失败 
var vm=new Vue({el:"#app"})   var vm1=new Vue({el:"#app2"})

※在vue实例中，如果要获取data上的数据或者调用methods中的方法，必须使用this.数据属性名 或this.方法名 来访问，this代表我们new出来的vm对象

※v-model="msg" msg是一个变量  如果后面要添加字符串 需要添加''引号来区别

※组件简写： login:login === login

※如果要传递点击事件  必须使用$event参数 传递进去

----------


1.v-cloak 等到页面加载完毕出现  

2.v-text 会覆盖原本中原本的位置  <p v-text="msg"></p> 不会解析标签

3.v-html 会展示内容的标签  会解析标签

4.v-bind:xx="xxxx"  这个是绑定属性  动态绑定属性  简写:xx="xxxx"   
 
5.v-on:click="xxx" 绑定事件     可以传入一个event事件参数: $event    简写@click="xxx"  注意：事件需要写在 methods:{xxx:function(){xx}}中   methods定义当前实例的所有可用方法  

6.使用计算属性  不需要声明 就可以使用变量  定义:computed:{msg()=>{ return xx}}   使用: {{msg}} 就可以返回

7.事件修饰符： @click.stop 防止冒泡  @click.prevent去除默认事件 @click.self 点击之身才触发回调函数         事件修饰符可以**串联**

8.v-model:双向数据绑定   <input v-model="msg">{{msg}}</p>   在vue里面唯一能够实现的:**表单**双向数据绑定的方法 只能运用在表单元素中

9.**使用class样式** 	第一种:数组 <h1 :class="['red','thin']"></h1>  		第二种:数组使用三元表达式  <h1 :class="['red','thin',isactibe？'actibe':'']"></h1>    
第三种:数组中镶嵌对象 <h1 :class="['red','thin',{'active':isactive}]"></h1>  **对象属性为类名  属性的值是一个标识符    键的值如果为true  那么就会使用这个类   如果为false就不会使用这个类 **    第四种：直接使用对象 <h1 :class="{red:true}"></h1>
**使用内联样式**  第一种：直接在元素上通过:style的形式,书写样式对象   <h1 ：style="{"color":'red'}"></h1>   第二种：将样式对象，定义到data种，并直接引用到:style种

10.v-for 循环: v-for="item in arr"     获取到索引值 v-for="(item,index) in arr"    in后面可以放 普通数组 对象数组 对象 数字  **放数字是代表循环多少次 数字是1 开始**
在组件中使用v-for循环的时候 必须加上 key    ** <my-component v-for="item in items" :key="item.id"></my-component>**   因为key是唯一标识  一般:key="item"  
key属性只能使用number或者string      key在使用的时候 必须使用v-bind属性绑定的形式，指定key值  items还可以是一个函数的返回值  searth(items) 相当于过滤器

11.v-if和v-show  v-if:没错都会删除或创建元素  v-show:每次不会重新删除和创建，只是改变display:none的值

12.定义vue过滤器   全局过滤器  语法： Vue.filter('过滤器的名称',function(data){})    注意：过滤器中的 function ，第一个参数，已经被规定死了，永远都是 过滤器 管道符前面 传递过来的数据  后面可以接受其他参数 		调用格式  {{ 需要过滤的数据 | 过滤器的名称 }}
私有过滤器  语法 实例化对象  filters:{		xxxx(){}	} //条件 [过滤器名称,处理函数]  过滤器是就近原则   如果私有和全局一样 那么优先调用私有

13.自定义键盘修饰符 Vue.config.f2=111  @keyup.f2=xxxx

14.自定义指令： Vue.directive('指令名',对象)       //定义全局指令 不需要添加v-但是在调用的时候 就必须v-前缀 参数2：是一个对象这个对象身上，有一些指令相关的函数，这些函数可以在特点的阶段执行相关的操作 对象里面有很多的内置函数 让我们使用 详情查阅**官方文档**  列举重要的几个: 
1. bind:function(el){}		 	//每当指令绑定到元素上的时候，会立即执行这个函数 只会执行一次      样式相关  
2. inserted:function(el){}		//表示元素插入到DOM中的时候 会执行inserted函数 只会执行一次   和js行为有关的在这里面实现
3. updated:function(el){} 		//当更新的时候，会执行updated	可能会触发多次
**在每一个函数中，第一个参数永远是el,表示 被绑定了指令的那个元素 可以直接操作DOM 这个el是一个原生的js对象  el=== <div></div> 所以el 等于我们获取的dom元素  el=== document.querySelector("xx")**
私有指令：directives:{'名字':{xxx}} 	简写私有化指令  'fontSize':function(el,binding){} //注意 这个fuction等同于将代码写到了bind 和update里面去了

15.vue实例的生命周期函数=生命周期函数=生命周期事件： 生命周期函数和el、data等平级

					/*这是组件创造建期间的生命周期钩子*/
 1. beforeCreate(){} 	//第一个生命周期函数  表示在实例化对象被创建之前	会执行它  **注意在beforeCreate生命周期函数执行的时候 data和methods中的数据都还没有初始化**
 2.	created(){}   //第二个生命周期函数   **表示初始化了data和methods的上面的数据**  如果要调用methods中的方法或者操作data中的数据 最早只能在created中去操作
 3.	beforeMount(){}  //表示模板已经在内存中编译完成了 但是尚未把模板渲染到页面中  在该函数被执行的时候  页面中的元素还没有被真正的替换过来，	只是之前写的一些 模板字符串
 4.	mounted(){} 	//表示已经把内存中的模板挂载到了页面上了  用户可以看见真实的页面 **从这里开始 就可以操作DOM了 虽然不推荐 但是这个地方是可以操作DOM的   如果要操作动态dom只能在这里操作**   该函数是实例创建期间的最后一个生命周期函数，当执行完该函数后 实例的就被完全创造好了 

					/*这是组件运行期间的生命周期钩子  根据data的数据变化，最少运行0次，最多无穷*/
 1. beforeUpdate(){}  //表示我们的界面还没有更新  但是数据已经更新了  也就是说 当数据更新的时候 就会触发该函数 但是 我们的界面还没有更新而已   **页面是旧的 data是最新的**
 2. updated(){} 	//执行的时候 页面和data数据已经保存同步了 都是最新的了  是让数据和页面同步

				/*这是组件销毁阶段的生命周期钩子  */
 1.	beforeDestroy(){} // 当执行该函数的时候，实例身上的所有data、所有的methods以及过滤器、指令都处于可用状态，此时还没有真正执行销毁过程
 2.	destroyed(){}  //执行该函数的时候，组件已经被全部销毁，此时组件的data和方法都为不可用状态

16.vue的Ajax请求：1.vue-resource  2.axios的第三方库   （只要是.then方法的都是使用的promise方法）
 1. vue-resource依赖与vue  **向vue实例挂载了一个方法：this.$http.get/post**  这个方法一般放在 creacted 也就是初始化参数的声明周期里面		如果我们通过全局配置了请求的数据接口 根域名 则每次单独发起HTTP请求的时候 请求的url路径 应该以相对路径开头  前面不能带/ 否者配置的根域名不会生效

17.vue动画效果： 使用过渡类名实现动画   <transition name="xx"> 	</transition>    **是谁需要过渡就包裹谁**

1. 使用transition 元素，把 需要被动画控制的元素 包裹起来  **注意这里的xx就是我们name的名字   只需要我们添加类名**  
2. 要使用样式  xxx-enter,.xxx-leave-to{} //这个是进场动画   v-enter：这是一个时间点  是进入之前，元素的起始状态  此时还没有开始进入    v-leave  是动画离开之后的终止状态，此时，元素 动画已经结束了  **位移效果就是在这里完成**
3. .xxx-enter-active,.xxx-leave-active    /* v-enter-active 入场动画时间段  */			 /* v-leave-active 离场动画时间段*/   

使用第三方库 完成动画效果：

1.	 <transition name="custom-classes-transition"  enter-active-class="animated tada" 	leave-active-class="animated bounceOutRight">   
2.	 注意：属性名称**enter-active-class   leave-active-class**  是跟的class  后面跟上动画名
3.	 动画的生命周期函数： **入场钩子函数** 
	 
  	v-on:before-enter="beforeEnter" //进入之前 设置起始状态

  	v-on:enter="enter"			 //进入

  	v-on:after-enter="afterEnter"	//进入之后

  	v-on:enter-cancelled="enterCancelled"//进入取消

 ** 定义函数**
  beforeEnter（el）{} //函数必须传递参数 el也就是我们绑定的那个DOM元素 是原生的js对象 
该函数是表示动画 入场之前， 此时动画没有开始 可以在该函数中 设置动画起始之前的样式

 enter（el，done）{
done()
} //该函数表示 动画开始之后的样式 这里可以设置小球完成动画之后的 结束状态
done 就是afterEnter函数 done是函数的引用

 afterEnter（el){}	//动画完成 之后执行

列表动画：transition-group包裹
 在实现列表过渡的时候，如果需要过度的元素是通过v-for循环渲染出来的，不能使用transition
包裹 需要是需要使用<transition-group></transition-group>  但是绑定的时候必须加上:key

加上进入的效果 <transition-group appear tag="指定渲染在上面元素上面">  加一个appear属性 实现入场效果 页面刚展示出来的时候 
删除离开动画效果过渡模板： .name-move{transition:all  0.6s} .name-leave-active{position:absolute}  必须这样完成

18.Vue组件：

1.定义全局组件
1.1 使用 var a=Vue.extend({ //创建全局组件
template:"" //通过template属性，指定了组件要展示的HTML结构
})
1.2 使用vue.component('组件名称',创建出来的组件模板对象)

		/**注意：可以直接使用vue.component('xx',{data: function () {
    return {
      count: 0
    }},template: '<button v-on:click="count++">You clicked me {{ count }} times.</button>'})**/
1.3使用组件的时候，自需要以标签的形式使用就可以了   **如果组件名是驼峰写法 那么引用的时候就需要把把大写字母用-链接起来 myA == my-A**

2.Vue.component('',{
template:'<div><a></a></div>'	//组件只能有唯一一个根元素
})
  
3.//但是这样写的方式太过于麻烦 那么就有一种方式 可以简化编写模板的过程
Vue.component('',{
template:'#app2',	//在模板里面指定我们绑定的元素
data:function(){   //data为一个函数 并且返回一个对象
	return {
msg:'xx'			//组件中的data数据，和实例中的data方式完全一样
}
}
})   

**然后在跟根元素的外面 新建一个模板然后指定id也就是我们在模板里面创建的id 就可以了**

    <div id="app"></div> <template id="app2"></template>

4.定义私有组件 
components:{
	login：{
	template:''
}
}

5.展示组件  vue提供conponent，来展示对应组件的名称
<component :is="用来指定要展示的组件的名称"></component> //组件名称要用''包裹起来 

6.组件的动画：不需要key 只需要定义动画名即可

	定义css样式
	 	.a-enter,.a-leave-to{
            opacity: 0;
            transform: translateY(-40px)
        }
        .a-enter-active,.a-leave-active{
            transition: all .5s ease
        }
 
    <transition name="a" model="out-in">  //自定动画名的名字  model可以指定2个组件的动画效果的先后顺序
                <com v-if="flag"></com>
                <com1 v-else></com1>
    </transition>

19.组件传值：
	
	1.父组件传值 ，可以在引用子组件的时候，通过属性绑定(v-bind:xx)的形式,把需要传递给子组件的数据 以属性绑定的形式传递到子组件内部，供子组件使用 
	<com :xxx="msg"></com> //	通过属性绑定的形式给子组件绑定了 一个xxx属性  他的值是msg   			父 ----> 子
	
	2.子组件接受父组件传递的数据，通过props来接受父组件传递过来的值，**名字必须和父组件传递过来的所绑定的属性一样  并且props是一个数组，里面的内容是一个字符串数组**
	com:{		
	data（）{	return{}	}，   //子组件中的data数据 并不是通过父组件传递过来的 而是子组件私有的 比如通过Ajax请求返回的数据，都可以放到data身上  **在组件中data必须是一个函数  data数据是可读可写的**

     template:'<h1>这是子组件-----{{parent}}</h1>',

     props:['parent'],//把父组件传递过来的parent属性，现在props数组中定义一下 这样才能使用数组     **props数据是只读的	无法重新赋值	**

            }
	
	3.父组件把方法传递给子组件：只能用事件绑定的方法（v-on:xxx="xx"）来给子组件传递方法 
		<com @xxx="msg"></com> //	通过属性绑定的形式给子组件绑定了 一个xxx的事件 
	然后在子组件中 使用 this.$emit('xxx'，参数1，参数2,......)  来触发父组件传递过来的方法  xxx必须和父组件传递过来的名字是一样的   并向父组件传参： **注意里面是一个字符串**
	
	4.子组件向父组件传递参数：使用Vue实例.$emit   来完成

20.获取元素（DOM）和组件
	<p ref="自己定义名字">123123</p>   
	
	methods:{
	aaa(){ //操作p标签内容 也就是操作DOM   
		this.$refs.我们定义的名字.dom操作事件
	}
	}
	
	<com ref="自己定义"></com>
	data(){return{a:a}}	



	aaa(){ //操作组件 也就是操作DOM   
		this.$refs.我们定义的名字.方法/属性
	}

30.路由：

1. 导入 vue-router 组件类库：

<!-- 1. 导入 vue-router 组件类库 -->
  <script src="./lib/vue-router-2.7.0.js"></script>
```
2. 使用 router-link 组件来导航
```
<!-- 2. 使用 router-link 组件来导航 -->
<router-link to="/login">登录</router-link>
<router-link to="/register">注册</router-link>
```
3. 使用 router-view 组件来显示匹配到的组件
```
<!-- 3. 使用 router-view 组件来显示匹配到的组件 -->
<router-view></router-view>
```
4. 创建使用`Vue.extend`创建组件
```
    // 4.1 使用 Vue.extend 来创建登录组件
    var login = Vue.extend({
      template: '<a>登录组件</a>'
    });

    // 4.2 使用 Vue.extend 来创建注册组件
    var register = Vue.extend({
      template: '<a>注册组件</a>'
    });
```
5. 创建一个路由 router 实例，通过 routers 属性来定义路由匹配规则
```
// 5. 创建一个路由 router 实例，通过 routers 属性来定义路由匹配规则   只能为routers  ** 注意：component 的属性值，必须是一个组件的模板对象，不能是组件的应用名称
Vue.compent('xx',{})  不能为xx xx只能用于html标签 只能使用组件的模板对象**
    var router = new VueRouter({
      routes: [
		{path:'/',redirect:'/login'}//重定向
        { path: '/login', component: login },
        { path: '/register', component: register }
      ]，
		linkActiveClass:'xxx',//自定义路由激活使用的样式
    });
```
6. 使用 router 属性来使用路由规则
```
// 6. 创建 Vue 实例，得到 ViewModel 在实例里面只能使用router来初始化
    var vm = new Vue({
      el: '#app',
      router: router // 使用 router 属性来使用路由规则
    });

7.使用路由激活样式： 在style中 对 .router-link-active类进行设置样式  就可以实现样式激活的时候 对其设置样式  这个类是vue 提供

8.路由传参： 
			query传参  用this.$route.query.xxx 来获取参数  不需要修改匹配规则

**多个参数中用&分隔 ‘foo?id=111&name=123'**
1.   <router-link to="/foo?'传递的属性名称'=10" >切换到第一个组件</router-link>   传递参数
2.   在组件中 使用	this.$route //可以输出 这个路由组件全部信息  然后在里面去读取内容
	this.$route.query.'传递的属性名称'  //获取传递的属性名 
3.	输出 <h1> {{this.$route.query.'需要获取的属性'}}</h1>    <h1> {{$route.query.'需要获取的属性'}}</h1>

		params传参  使用this.$route.params.xx 来获取参数  需要修改匹配规则
 1.  {path:'/foo/:id',component:A}	//说明在组件中需要传入一个值
 
 2.   <router-link to="/foo/10" >切换到第一个组件</router-link>   //在组件传入了一个值

 	 this.$route.params.'我们在路由规则里面定义的参数'  就可以获取到值 
	

**<!--路由传参可以传递变量 但是必须使用令名路由     也就是 需要在 {path:'/foo/:id',component:A,name:'id'}   注册名字   然后使用--  <router-link ：to="{name:'id',parems:{id:我们需要传入的变量}}"    然后就可以获取去了  注意 这里的to是属性绑定的方法 >>**

31,路由嵌套： 使用children来实现子路由的嵌套  ：注意不能到/

	`<router-link to="/parent/a">a组件</router-link>` 
	<router-view></router-view>
	
	  {path:'/parent',component:parent,
        children:[
            {path:'a',component:children1},
            {path:'b',component:children2}
        ]},

32.命名视图：同级展示多个视图
	

	` // 多命名识图路由 组件是带components  带s的  必须带有多个组件
        {path:'/',name:'a',components:{
            default:box, //不写就是默认展示的组件
            a:box2,//需要展示的组件的名称
            b:box3
        }},`
      <router-view name="a"></router-view>   <router-view name="b"></router-view>

33.watch监听属性：可以监听data中指定数据的变化，然后触发watch中对应的function 处理函数。可以不用触发methods里面的方法都可以使用

	` watch:{//使用这个属性可以 监视data中指定数据的变化，然后触发watch中对应的function处理函数
            a(newVal,oldVal){//这个是指定监视的元素  该函数带有2个参数 参数可选
                    console.log('触发了监听事件')
            },
			'$router.path'(){//监听路由参数的改变
			}

        }`
可以监听路由 路径的改变  $router.path 

34.计算属性：在这个属性中，可以定义一些属性，这些属性叫做计算属性， 其本质是一个方法，只不过我们，我们在使用这些计算属性的时候，是把他们的名称当作属性来使用的，并不会把计算属性，当作方法去调用

不需要在data里面去定义  是直接在computed：{}里面定义的

**注意：计算属性 在引用的时候 一定不要加()去调用，直接把它当作普通属性去使用接可以了**

**只要 计算属性，这个function内部，所用到的任何data中的数据发送了变化，就会立刻重新计算 这个 计算属性的值**

**计算属性的求值结果，会被缓存起来，方便下次直接使用；如果计算属性方法中，所有用的任何数据，都没有发生过变化 则 不会重新对 计算属性求值**
	
	` computed:{//在这个属性中，可以定义一些属性，这些属性叫做计算属性， 其本质是一个方法，只不过我们，我们在使用这些计算属性的时候，
       //是把他们的名称当作属性来使用的，并不会把计算属性，当作方法去调用
            c(){
                return this.a+'-'+this.b //一定要有return
            }
       }`


35.render函数：

	` render:function(createElements){ //vue提供的参数 替换模板显示
            return createElements(login)  //替换el指定的那个容器 
        }`


36.使用solt

	https://www.cnblogs.com/chinabin1993/p/9115396.html	
	也就是可以在组件中写东西
	
	














##vue+Webpack结合使用
1. 使用npm i vue -S 安装包
2. 引入 vue包 如果直接使用import vue from 'vue' 是一个阉割版   会报错 有三种解决方式
	1. 修改vue目录下的package.json 文件 ，修改main的路径指向vue.js
	
	`"main": "dist/vue.runtime.common.js",
 	 "module": "dist/vue.runtime.esm.js",`
	2. 修改我们引包的路径 
	`import Vue from '../node_modules/vue/dist/vue.js'
		`
	3. 在webpack.config.js配置文件中新增一个节点模块

	`resolve:{//添加节点
        alias:{
            "vue$":'vue/dist/vue.js' //以vue结尾的文件都指向我们定义的目录
        }
    }`
3. webpack无法打包.vue文件，需要安装相关的loader
	1.npm i vue-loader 	 vue-template-compiler -D  vue-laoder内部依赖 vue-template-compiler

	2.然后在配置文件配置

	`const {VueLoaderPlugin}=require("vue-loader") //引入插件
	module:{
		rules:[
		{
		test:/\.vue$/,
		use:'vue-loader',
		}
			]
	},
	plugins:[
	new VueLoaderPlugin() //实例化插件
	] `

4.使用vue-router模块

	1.  安装npm i vue-router 
	2.  引包、
		import VueRouter from 'vue-router'
	3.  实例化路由
		`vue.use(VueRouter)`



##在.vue文件中
1. 需要使用  export default来暴露数据
	
	`export default {
    data(){ //组件中必须为function
        return{

        }
    },
    methods:{
        show(){
            console.log("调用了组件的方法")
        }
    },
    created(){
        this.show()
    }
}`






git合并分支:
git pull origin master



路由传参最常用：
:to="{
        path: 'yourPath', 
        params: { 
            name: 'name', 
            dataObj: data
        },
        query: {
            name: 'name', 
            dataObj: data
        }
    }">

	:to="'/home/newInfo/'+index" //凭借字符串






----------
// node中向外暴露成语的形式
// module.exports={} 和exports 暴露成员
// const 名称=require("模块标识符") 导入模块




// 在es6中，也通过规范的形式，规定了es6中如何 导入和 导出模块
// ES6中导入模块 使用 import 模块名称 from "模块标识符" ----> js代码相关  import "表示路径" ---->非js代码相关
// 在es6中，使用export default 和export 向外暴露成员：
//	在一个模块中可以同时使用  export default 和 export 

    export default {  //向外暴露的成员 可以使用任意的变量来接受  一个js文件里面中，只运行向外暴露一次 也就是只能有一个
    	xxxxxx                                     
    }
	=============
	var xxx=123;
	export default xxx;

	import 任意变量来接受 from '路径'

	export var 变量名=`12  //使用exprot 暴露的成员只能使用{1,2,3}的形式接受，叫做按需导出 多个使用 ，隔开 可以暴露多个成员
	import {变量名} from 'xxxx'  二者变量名必须一样
	
