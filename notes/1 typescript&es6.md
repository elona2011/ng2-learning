# Typescript and ES6
angular2采用typescript语法和ES6 ，比较常用的有：

## 箭头函数
chrome的调试窗口中箭头函数中的this会显示为指向Window，该显示是错误的，实际指向class

## let
```
for(var i=1;i<5;i++){
 setTimeout(function timer(){
  console.log(i);
 },i*1000);
} //输出4个5

for(let i=1;i<5;i++){
 setTimeout(function timer(){
  console.log(i);
 },i*1000);
} //输出1，2，3，4
```

## class
```
export class Hello {//定义类和构造函数
    name: string = 'World';
    constructor() {
        setTimeout(() => {
          this.name = 'NEW World'
        }, 2000);
    }
}
```
Constructor构造函数，初始化数据

# 参考：
http://www.typescriptlang.org/Handbook
http://es6.ruanyifeng.com/