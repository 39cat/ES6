var arr = ['a','b','c','d'];


for (let a in arr){
  console.log(a);//0,1,2,3
}

for(let a of arr){
   console.log(a);//a,b,c,d
}