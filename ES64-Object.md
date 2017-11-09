对象的扩展

1.属性的简洁表示法：
   例：let birth = '2000/01/01';
		const Person = {
		  name: '张三',
		  //等同于birth: birth
		  birth,
		  // 等同于hello: function ()...
		  hello() { console.log('我的名字是', this.name); }
		};
2.属性名表达式：
   例：
      // 方法一
		obj.foo = true;

	  // 方法二
		obj['a' + 'bc'] = 123;(表达式可以作为属性名)
		
	用法：例1：
			let lastWord = 'last word';
			const a = {
			  'first word': 'hello',
			  [lastWord]: 'world'
			};

			a['first word'] // "hello"
			a[lastWord] // "world"
			a['last word'] // "world"
		   例2：
		     let obj = {
			  ['h' + 'ello']() {
				return 'hi';
			  }
			};

			obj.hello() // hi
			
     注意：属性名表达式与简洁表示法，不能同时使用，会报错。
   
3.方法的name属性（返回函数名）
     例：
       const person = {
			  sayName() {
				console.log('hello!');
			  },
			};
			person.sayName.name   // "sayName"
   
4.Object.is(比较两个值是否相等)

    例子以及优点：
	   +0 === -0 //true
		NaN === NaN // false

		Object.is(+0, -0) // false
		Object.is(NaN, NaN) // true
     注："=="与"==="前者会自动转换数据类型，后者的NaN不等于自身，以及+0等于-0
   ES5实现方式：
      Object.defineProperty(Object, 'is', {
			  value: function(x, y) {
				if (x === y) {
				  // 针对+0 不等于 -0的情况
				  return x !== 0 || 1 / x === 1 / y;
				}
				// 针对NaN的情况
				return x !== x && y !== y;
			  },
			  configurable: true,
			  enumerable: false,
			  writable: true
			});
			
	 
   说明：Object.defineProperty(将属性添加到对象，或修改现有属性的特性)
            Object.defineProperty(object, propertyname, descriptor)
             1> object
				   必需。  要在其上添加或修改属性的对象。  这可能是一个本机 JavaScript 对象（即用户定义的对象或内置对象）或 DOM 对象。  
			  	propertyname
				   必需。  一个包含属性名称的字符串。  
				descriptor
				   必需。  属性描述符。  它可以针对数据属性或访问器属性。  
			  2>Configurable:表示能否通过delete删除属性从而重新定义属性；
				Enumerable：表示能否通过for-in循环返回属性
				writable：表示能否修改属性的值
				Value：包含这个属性的数据值（个人认为其作用就是赋值）
   
5Object.assign(对象的合并)
    例： 以第一个为目标，把后面的对象合并到第一个对象  
	    const target = { a: 1 };

		const source1 = { b: 2 };
		const source2 = { c: 3 };

		Object.assign(target, source1, source2);
		target // {a:1, b:2, c:3}
   注意：
     1>如果出现同名属性，后面的会覆盖前面的
         例：    
			const target = { a: 1, b: 1 };

			const source1 = { b: 2, c: 2 };
			const source2 = { c: 3 };

			Object.assign(target, source1, source2);
			target // {a:1, b:2, c:3}
	 2>如果只有一个参数，Object.assign会直接返回该参数
	    例：  
		   const obj = {a: 1};
		   Object.assign(obj) === obj // true
		   
	 3>对数组的处理：(把数组视为对象。)
         Object.assign([1, 2, 3], [4, 5]);  // [4, 5, 3]
		 
    用途：（稍后补充）
	   1>为对象添加属性
	   2>为对象添加方法
	   3>克隆对象
	   4>合并多个对象

6：属性的遍历：
     ES6 一共有5种方法可以遍历对象的属性。

		（1）for...in
			 for...in循环遍历对象自身的和继承的可枚举属性（不含 Symbol 属性）。

		（2）Object.keys(obj)
			 Object.keys返回一个数组，包括对象自身的（不含继承的）所有可枚举属性（不含 Symbol 属性）的键名。

		（3）Object.getOwnPropertyNames(obj)
			 Object.getOwnPropertyNames返回一个数组，包含对象自身的所有属性（不含 Symbol 属性，但是包括不可枚举属性）的键名。

		（4）Object.getOwnPropertySymbols(obj)
			 Object.getOwnPropertySymbols返回一个数组，包含对象自身的所有 Symbol 属性的键名。

		（5）Reflect.ownKeys(obj)
			 Reflect.ownKeys返回一个数组，包含对象自身的所有键名，不管键名是 Symbol 或字符串，也不管是否可枚举。
	
	属性的枚举：
		let obj = { foo: 123 };
		Object.getOwnPropertyDescriptor(obj, 'foo')
		//  {
		//    value: 123,
		//    writable: true,
		//    enumerable: true,
		//    configurable: true
		//  }
7：Object.keys()，Object.values()，Object.entries()	 