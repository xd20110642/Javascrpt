#接口
	1.接口就是声明一个对象里面的数据类型
	interface Person{
		firstname:String;
		lastname:Number
	}
	
#类
		
		class Student {
    fullName: string;//这个是先声明 能变量 就相当于 下面
    constructor(public firstName, public middleInitial, public lastName) {
        this.fullName = firstName + " " + middleInitial + " " + lastName;
    }
	}
	
	funtion Person(aaa){
	//sss 就相当于 上面的 fullName
		this.sss=aaa
	}
#声明数据类型
	1. 变量:数据类型
	2. 数组
		1.arr:number[]=[1,2,3]//声明一个全是数字的对象
		2.arr:Array<number> //同上
		3.元祖  元组类型允许表示一个已知元素数量和类型的数组，各元素的类型不必相同。
			let x:[string,boolean]
	3.枚举  就是提前封装一些内容 降低耦合  也必须是对象   就是提供 常量
		eum Color{
			Gree,
			
			
		}
				
			