数值的扩展

 1.Number.isNaN(检查一个值是否为NaN):
      例：Number.isNaN(2) // false
 2.Number,isFinte(检查一个数值是否是有限的)
      例：Number.isFinite(0.2) // true
 3.Number.parseInt(),Number.ParseFloat()
      ES6 将全局方法parseInt()和parseFloat()，移植到Number对象上面，行为完全保持不变
 4.Number.isInteger(判断一个值是否是一个整数)
      例：Number.isInteger(0.3) // false
 5.Math.trunc(返回整数部分)
      例：Math.trunc(12.18) // 12
 6.Math.sign(判断一个数是正数，负数，还是0)
     参数为正数，返回+1；  Math.sign(5) // +1     ==>Math.sign(true)  // +1
     参数为负数，返回-1；  Math.sign(-5) // -1
     参数为0，返回0；      Math.sign(0) // +0     ==> Math.sign(null | false | "") // 0
     参数为-0，返回-0;     Math.sign(-0) // -0
     其他值，返回NaN。     Math.sign(NaN) // NaN  ==> Math.sign('foo' | undefined |  )  // NaN
 7.Math.cbrt(计算一个数的立方根)
     例：Math.cbrt('8') // 2
 8.Math.hypot(所有参数的平方和 的 平方根)
     例： Math.hypot(3, 4); // 5  （3的平方加上4的平方，等于5的平方）