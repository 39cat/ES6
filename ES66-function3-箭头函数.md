箭头函数 
   例：
     1>如果箭头函数不需要参数或需要多个参数，就使用一个圆括号代表参数部分。
		var f = () => 5;
		// 等同于
		var f = function () { return 5 };

		var sum = (num1, num2) => num1 + num2;
		// 等同于
		var sum = function(num1, num2) {
		  return num1 + num2;
		};	  
      2>如果箭头函数的代码块部分多于一条语句，就要使用大括号将它们括起来，并且使用return语句返回。
	    var sum = (num1, num2) => { return num1 + num2; }
	  3>如果箭头函数直接返回一个对象 如：
			// 报错
			let getTempItem = id => { id: id, name: "Temp" };		
		必须在对象上加()
		  // 不报错
		 let getTempItem = id => ({ id: id, name: "Temp" });
    优点：
	   1>可以和结构赋值用，使表达更加简洁
	      例：
			const full = ({ first, last }) => first + ' ' + last;

			// 等同于
			function full(person) {
			  return person.first + ' ' + person.last;
			}		
		2>简化回调函数
		   例：
		     // 正常函数写法
			[1,2,3].map(function (x) {
			  return x * x;
			});

			// 箭头函数写法
			[1,2,3].map(x => x * x);
		3>还可以和rest参数结合：
          例：
            const headAndTail = (head, ...tail) => [head, tail];
            headAndTail(1, 2, 3, 4, 5)  //	// [1,[2,3,4,5]]	  
    注意：
	    （1）函数体内的this对象，就是定义时所在的对象，而不是使用时所在的对象。
              例：
			    function Timer() {
				  this.s1 = 0;
				  this.s2 = 0;
				  // 箭头函数
				  setInterval(() => this.s1++, 1000);
				  // 普通函数
				  setInterval(function () {
					this.s2++;
				  }, 1000);
				}

				var timer = new Timer();

				setTimeout(() => console.log('s1: ', timer.s1), 3100);
				setTimeout(() => console.log('s2: ', timer.s2), 3100);
				// s1: 3
				// s2: 0
				这个例子说明箭头函数导致this总是指向函数定义生效时所在的对象
				在那里定义的，this就指向那里
				
		（2）不可以当作构造函数，也就是说，不可以使用new命令，否则会抛出一个错误。

		（3）不可以使用arguments对象，该对象在函数体内不存在。如果要用，可以用 rest 参数代替。

		（4）不可以使用yield命令，因此箭头函数不能用作 Generator 函数。

    晋级：
	    箭头函数的嵌套

2双冒号运算符
	1>函数绑定运算符是并排的两个冒号（::），双冒号左边是一个对象，右边是一个函数。
	  该运算符会自动将左边的对象，作为上下文环境（即this对象），绑定到右边的函数上面。
		 例：
			foo::bar;
			// 等同于
			bar.bind(foo);

			foo::bar(...arguments);
			// 等同于
			bar.apply(foo, arguments);
    2>如果双冒号左边为空，右边是一个对象的方法，则等于将该方法绑定在该对象上面。
			例：
			    var method = obj::obj.foo;
				// 等同于
				var method = ::obj.foo;

				let log = ::console.log;
				// 等同于
				var log = console.log.bind(console);
    3>双冒号运算符的运算结果，还是一个对象，因此可以采用链式写法。
		      // 例一
				import { map, takeWhile, forEach } from "iterlib";

				getPlayers()
				::map(x => x.character())
				::takeWhile(x => x.strength > 100)
				::forEach(x => console.log(x));

				// 例二
				let { find, html } = jake;

				document.querySelectorAll("div.myClass")
				::find("p")
				::html("hahaha");



					
		
		
		
		
		