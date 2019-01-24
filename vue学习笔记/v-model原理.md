#v-model原理
	v-model等于
	<innput v-model="something">
		<===>
	<input :value="something" @input="something = $event.target.value">
#在组件上使用v-model 原理也是一样的 
##组件上的v-model默认利用的是v
	整体情况
	<custom-input v-model="xxx"></custom-input>
	
		<===>
		<!--拆分-->
		<!--父组件向子组件传值 -->
		<custom-input
 		 v-bind:value="searchText"
  		v-on:input="searchText = $event"
		></custom-input>	
		//这个是子组件内部的
			Vue.component('custom-input', {
	  props: ['value'],
	  template: `
	    <input
	      v-bind:value="value"
	      v-on:input="$emit('input', $event.target.value)"
	    >
	  	`
		})