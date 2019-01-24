1.利用v-for 获取到当前索引值的方法             index就是我们当前的索引值 
 			     <tr v-for="(item,index) in list" >												 `this.list.splice(index,1) ` 这个地方是数组删除指定地方的元素
				    <td>{{item.id}}</td>
				    <td>{{item.name}}</td>
				    <td>{{item.ctime}}</td>
				    <td><a @click="remove(index)">删除</a></td>
				  </tr>
				  
2.在vue绑定事件中，如果方法带了小括号 那么就是可以传参

3.对$nextTick方法的理解
	
		我常用的场景是在进行获取数据后，需要对新视图进行下一步操作或者其他操作时，发现获取不到dom。因为赋值操作只完成了数据模型的改变并没有完成视图更新。
		
			
			new Vue({
		  el: '#app',
		  data: {
		    list: []
		  },
		  mounted: function () {
		    this.get()
		  },
		  methods: {
		    get: function () {
		      this.$http.get('/api/article').then(function (res) {
		        this.list = res.data.data.list
		        // ref  list 引用了ul元素，我想把第一个li颜色变为红色
		        this.$refs.list.getElementsByTagName('li')[0].style.color = 'red'
		      })
		    },
		  }
		})
		
		
		
		
		我在获取到数据后赋值给数据模型中list属性，然后我想引用ul元素找到第一个li把它的颜色变为红色，但是事实上，这个要报错了，我们知道，在执行这句话时，ul下面并没有li，也就是说刚刚进行的赋值操作，当前并没有引起视图层的更新。因此，在这样的情况下，vue给我们提供了$nextTick方法，如果我们想对未来更新后的视图进行操作，我们只需要把要执行的函数传递给this.$nextTick方法，vue就会给我们做这个工作
		
		
参考链接:https://www.cnblogs.com/xujiazheng/p/6852124.html		