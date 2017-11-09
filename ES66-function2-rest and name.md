rest参数
  获取函数多余参数，搭配的是一个数组，将多余参数放到其中
  例：  
		function add(...values) {
		  let sum = 0;

		  for (var val of values) {
			sum += val;
		  }

		  return sum;
		}

		add(2, 5, 3) // 10
	作用：
	 例1：可以替代arguments变量
	    // arguments变量的写法,arguments不是数组，是一个类似数组的对象
			function sortNumbers() {
			  return Array.prototype.slice.call(arguments).sort();
			}

			// rest参数的写法
			const sortNumbers = (...numbers) => numbers.sort();
	 例2：push 参数
        	function push(array, ...items) {
			  items.forEach(function(item) {
				array.push(item);
				console.log(item);
			  });
			}

			var a = [];
			push(a, 1, 2, 3) 
	  注意：
	     1>rest必须是最后一个参数
		 2>函数的length是不包括reset的
		 
函数的name（函数的name属性，返回该函数的函数名。）
     例：function foo() {};  foo.name // "foo"
	 注意： 
        1：ES5里name属性返回空字符串
        2：具名函数赋值给一个变量，ES5和ES6都返回具名函数的名称
            例：
               	const bar = function baz() {};
				// ES5
				bar.name // "baz"
				// ES6
				bar.name // "baz"	
        3：Function构造函数返回的函数实例，name属性的值为anonymous。		
		   例：	(new Function).name // "anonymous"
		4：	bind返回的函数，name属性值会加上bound前缀。
		  例： 
		   function foo() {};
		   foo.bind({}).name // "bound foo"

		   (function(){}).bind({}).name // "bound "		