函数的扩展

1.函数参数的默认值
  1.1基本用法：
     直接写在参数的定义后面
	 例：
	    function log(x, y = 'World') {
		  console.log(x, y);
		}

		log('Hello') // Hello World
		log('Hello', 'China') // Hello China
		log('Hello', '') // Hello
	注意：
	    1>使用参数默认值时，函数不能由同名参数
		2>参数默认值不是传值的，而是每次都重新计算默认值表达式的值。也就是说，参数默认值是惰性求值的
		  例：  let x = 99;
				function foo(p = x + 1) {
				  console.log(p);
				}

				foo() // 100

				x = 100;
				foo() // 101
	1.2与解构赋值默认结合使用
         例：
			function foo({x, y = 5}) {
			  console.log(x, y);
			}

			foo({}) // undefined 5
			foo({x: 1}) // 1 5
			foo({x: 1, y: 2}) // 1 2
			foo() // TypeError: Cannot read property 'x' of undefined	
      注意：
		只有当函数foo的参数是一个对象时，变量x和y才会通过解构赋值生成。
		如果函数foo调用时没提供参数，变量x和y就不会生成，从而报错，
		通过提供函数参数的默认值，就可以避免这种情况。
		例子：
			function foo({x, y = 5} = {}) {
			console.log(x, y);
			}

			foo() // undefined 5	
      考题1：
	       function fetch(url, { body = '', method = 'GET', headers = {} }) {
			  console.log(method);
			}

			fetch('http://example.com', {})
			// "GET"

			fetch('http://example.com')
			// 报错
		解决：
			function fetch(url, { body = '', method = 'GET', headers = {} } = {}) {
			console.log(method);
			}

			fetch('http://example.com')
			// "GET"
	    考题2：区别是:
		          写法一函数参数的默认值是空对象，但是设置了对象解构赋值的默认值；
		          写法二函数参数的默认值是一个有具体属性的对象，但是没有设置对象解构赋值的默认值。
		    // 写法一：x,y都有默认值
			function m1({x = 0, y = 0} = {}) {
			  return [x, y];
			}

			// 写法二{x,y}有默认值
			function m2({x, y} = { x: 0, y: 0 }) {
			  return [x, y];
			}
				
			// 函数没有参数的情况
			m1() // [0, 0]
			m2() // [0, 0]

			// x 和 y 都有值的情况
			m1({x: 3, y: 8}) // [3, 8]
			m2({x: 3, y: 8}) // [3, 8]

			// x 有值，y 无值的情况
			m1({x: 3}) // [3, 0]
			m2({x: 3}) // [3, undefined] //写法二因为有传值，所以不适应默认值，

			// x 和 y 都无值的情况
			m1({}) // [0, 0];
			m2({}) // [undefined, undefined]

			m1({z: 3}) // [0, 0]
			m2({z: 3}) // [undefined, undefined]	
				
		参数默认值的位置：
          1>定义了默认值的参数，应该是尾参数
          2>非尾参数定义默认值，这个传递的参数不能为空应该传undefined	
            例：		  
				function f(x, y = 5, z) {
				  return [x, y, z];
				}

				f() // [undefined, 5, undefined]
				f(1) // [1, 5, undefined]
				f(1, ,2) // 报错
				f(1, undefined, 2) // [1, 5, 2]				
								
		注意：传入undefined，将触发该参数等于默认值，null则没有这个效果
			例：		
			function foo(x = 5, y = 6) {
			  console.log(x, y);
			}

			foo(undefined, null)
			// 5 null				
	函数的lenth属性
        1>函数设置默认参数后length属性将失真
          例：(function (a, b, c = 5) {}).length // 2	   
		2>函数rest 参数也不会计入length属性。
          例：(function(...args) {}).length // 0
        3>如果设置了默认值的参数不是尾参数，那么length属性也不再计入后面的参数了
          例：(function (a, b = 1, c) {}).length // 1
    参数默认值作用域
        先是当前作用域，后是全局作用域
		 例1：
			var x = 1;
			function foo(x, y = function() { x = 2; }) {
			  var x = 3;
			  y();
			  console.log(x);
			}

			foo() // 3
			x // 1
			
			注解：由于默认传值foo(这里是一个单独的作用域，(x = 2)里的x指向第一个参数x)
			      而foo(){console.log(x)里的x指向的是var x = 3 }
		例2：
							
			var x = 1;
			function foo(x, y = function() { x = 2; }) {
			  x = 3;
			  y();
			  console.log(x);
			}

			foo() // 2
			x // 1				
			注解：由于默认传值foo(这里是一个单独的作用域，(x = 2)里的x指向第一个参数x)
			      而foo(){console.log(x)里的x指向的是 "x=3" ,而"x=3"的x也是指向第一个参数的x}
    函数参数的默认值应用：
      1：利用参数默认值，可以指定某一个参数不得省略，如果省略就抛出一个错误
         例：		
			function throwIfMissing() {
			  throw new Error('Missing parameter');
			}

			function foo(mustBeProvided = throwIfMissing()) {
			  return mustBeProvided;
			}

			foo()
			// Error: Missing parameter	
		2：	将参数默认值设为undefined，表明这个参数是可以省略的	
		   例：function foo(optional = undefined) { ··· }
	   