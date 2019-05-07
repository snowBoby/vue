# vue
vue原理

vue三要素：
  1、vue中如何实现响应式：
    响应式就是修改data属性之后，vue会立刻监听到，data属性被代理到vm上，通过Object.defineProperty方法来实现的。
    
		var obj = {age:19}
		Object.defineProperty(obj,'name',{
			get:function(){
				console.log(name)
				return name
			},
			set:function(newval){
				console.log(newval);
				name = newval
			}
		})
		data属性被代理到vm上：
		var vm = {},obj={name:'ahsh',age:19}
		for(var key in obj){
			(function(key){
				if(obj.hasOwnProperty(key)){
					Object.defineProperties(vm,key,{
				        get:function(){
				            return data[key]
				        },
				        set:function(newval){
				            data[key] = newval
				        }
				    })
			    }
			})(key)
		}
  
  2、vue中如何解析模板：
		模板就是一个字符串，最终必须转化成js代码，因为有逻辑（v-if v-for）,必须用js才能实现（图灵完备），同时要转化为html
		渲染页面，必须用js才能实现，因此，模板最终要转化成js函数（render函数）
    render函数：
      模板中所有信息都包含在了render函数中，this指的是vm
    render函数里面的with的使用：
      var obj = {
        name:"gao",
        age:18,
        say(){
          console.log(1111)
        }
      }
      function fn(){
        console.log(obj.name);
        console.log(obj.age);
        console.log(obj.say());
      }
      
      with的写法：
      function fn1(){
        with(obj){
          console.log(name);
          console.log(age);
          console.log(say());
        }
      }
      


      
      
      
      
      
      
