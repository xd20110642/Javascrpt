#element UI框架使用技巧
1. 配置表单校验规则
	
		在form属性上配置rules（表单验证规则） 
		<el :model="pageForm" :rules="pageFormRules" ></el>
		然后在数据模型中配置校验规则
		pageFormRules:{
		siteId:[
			{required:true,message:'请选择站点',trigger:'blur'}
		]
			
		}
		如果要触发点击按钮触发校验,需要在form表单上添加ref属性,在校验时引用此表单对象
		<el‐form :model="pageForm" :rules="pageFormRules" label‐width="80px" ref="pageForm">
		<!--传入的参数为我们自定义的表单校验规则-->
		<button @click=自定义事件()></button>
		
		方法:
		this.$refs.pageForm.validate((valid) => {
			 if (valid) {
			})
			alert('提交'); } else {
			alert('校验失败');
			  return false;
			}
		})