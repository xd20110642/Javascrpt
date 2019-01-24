##vue路由跳转

1. 使用a标签的形式叫做 标签跳转
2. 使用window.location.href的形式，叫做编程式导航


##route 和router 的区别
1. this.$route 是路由参数对象，所有路由中的参数，params,query都属于他
2. this.$router是一个路由导航对象，用它 可以方便的使用js代码，实现路由的前进、后退、跳转刷新URL地址

this.$router.psuh() //跳转

this.$router.go(-1) //返回 