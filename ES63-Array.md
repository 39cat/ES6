数组的扩展
 
  1.扩展运算符
    1.1.1(spread)(讲一个数组转化为用逗号分隔的参数序列)
			   例：console.log(...[1,2,3]);                  //1,2,3
				   console.log(1,...[2,3,4],5);              //1,2,3,4,5
				   [...document.querySelectorAll("div")]     // [<div>,<div>,<div>]
	1.1.2作用：
	      1>替代数组的apply方法：
                例1：ES5写法
				   function f(x,y,z){
				     
				    }
					var args = [0,1,2];
					f.apply(null,args);
					ES6写法：
					function f(x,y,z){
				     
				    }
					var args = [0,1,2];
					f.apply(...[args]);
                 例2push方法
                     // ES5的 写法
						var arr1 = [0, 1, 2];
						var arr2 = [3, 4, 5];
						Array.prototype.push.apply(arr1, arr2);

					// ES6 的写法
						let arr1 = [0, 1, 2];
						let arr2 = [3, 4, 5];
						arr1.push(...arr2);	
            2>复制数组(spread)自带复制功能
                   例：//ES5写法：
                         const a1 = [1,2];
                         const a2 = a1.concat();(concat(),合并一个数组，生成一个新数组，a1.concat()就是把原来的复制一下)
                       //ES6写法： 
                         const a1 = [1,2];
                         //写法一
                            const a2 = [...a1];
                         //写法二
                            const [...a2] = a1;		
             3>合并数组
                   例：//ES5写法：a1.concat(a2,a3);
                       //ES5写法：[...a1,...a2,...a3];
             4>字符串：
                   例：[..."hello"] //["h","e","l","l","e"],			 
      
  2.数组的转换
      2.1Array.from(将类似数组对象和可遍历的对象转化为数组)
	     例：let arrayLike = {
					'0': 'a',
					'1': 'b',
					'2': 'c',
					length: 3
				};

				// ES5的写法第一种写法
				var arr1 = [].slice.call(arrayLike); // ['a', 'b', 'c']

				//第一种写法 var arr1 = Array.prototype.slice.call(arrayLike);

				// ES6的写法
				let arr2 = Array.from(arrayLike); // ['a', 'b', 'c']
	      注意：可以接受两个参数 （第二个参数用于对每个参数进行操作）
                  例：Array.from(arrayLike, x => x * x);	
	           类似于数组的map方法
				   例：Array.from(arrayLike).map(x => x*x);
	  
      2.2Array.of(将一组值转换为数组)
           例：Array.of(1,2,3)   //[1,2,3]
         Array.of()原理：
                  function ArrayOf(){
				  return [].slice.call(arguments);
				}		 
	 
	  2.3copyWithin(copy"自己"指定位置的成员到"自己"其他位置)
	       Array.prototype.copyWithin(target, start = 0, end = this.length)
	        1>target（必需）：从该位置开始替换数据。
			2>start（可选）：从该位置开始读取数据，默认为0。如果为负值，表示倒数。
			3>end（可选）：到该位置前停止读取数据，默认等于数组长度。如果为负值，表示倒数。
	      注意：copyWithin()是改变自身的函数
		     例：[1,2,3,4,5].copyWithin(0,3);  //[4,5,3,4,5](改边自身)
	  2.4fand()和findIndex()
	     2.4.1find(找出第一个符合条件的数组成员(参数是一个回调函数))
	         例：[1,4,-5,10].find((n) => n<0);  //-5 (找出数组中第一个小于0的成员)
	     2.4.2findIndex(第一个符合条件的数组成员的位置，如果所有成员都不符合条件，则返回-1)
		     例：[1,5,10,15].findIndex((n) => n>10); //3
           优点：这两个方法都可以发现NaN，弥补了数组的IndexOf方法的不足	 
	         例： 
					[NaN].indexOf(NaN)
				// -1 （不能识别NaN）
				
				[NaN].findIndex(y => Object.is(NaN, y))
				// 0  （识别NaN）
	  2.5fill(fill方法使用给定值，填充一个数组)
	      例：['a', 'b', 'c'].fill(7) //['7','7','7']
		      可以接受第二个和第三个参数用于指定填充的起始位置和结束位置
		      ['a','b,'c'].fill(7,1,2) //['a','7','7']
	     注意：当第三个参数超出length 不会改变数组长度，只到最后一个
	  2.6entries()，keys() 和 values()
	      keys()是对键名的遍历、values()是对键值的遍历，entries()是对键值对的遍历。
		  可以配合for...of使用
	     例：for (let index of ['a', 'b'].keys()) {
			  console.log(index);
			}
			// 0
			// 1

			for (let elem of ['a', 'b'].values()) {
			  console.log(elem);
			}
			// 'a'
			// 'b'

			for (let [index, elem] of ['a', 'b'].entries()) {
			  console.log(index, elem);
			}
			// 0 "a"
			// 1 "b"
	
	  2.7inclides(返回一个布尔值（示某个数组是否包含给定的值，与字符串的includes方法类似）)
	      例：
				[1, 2, 3].includes(2)     // true
				[1, 2, 3].includes(4)     // false
				[1, 2, NaN].includes(NaN) // true  