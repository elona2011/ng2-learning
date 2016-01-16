# 事件
## 系统事件
click事件
```
<div (click)="toggle()">
```
(click)监听click事件
toggle()事件触发函数
```
<div [hidden]="!visible">
```
[hidden] 中括号将HTML元素或组件的属性绑定到组件模型的某个表达式，当表达式的值变化时，对应的DOM对象将自动得到更新。
visible为对应class中定义的变量
keyup事件
例：``<input class="form-control" type="text" placeholder="Your new friend" #friend (keyup) ="update(friend.value)">``
键盘事件
1.document方法：
将下面代码加入class的constructor中
```
document.onkeydown = function(event) {
  switch (event.keyCode) {
    case 38:
      alert('clear');
      break;
  }
}
```

2.window方法：
将下面代码加入class的constructor中

```
window.addEventListener("keydown",()=>{
//1、显示miniepg
if (window.event && window.event.which === 73) {
this.showFlag = true;
}
}, true);
```

3.Angular2方法：
1.import
```
import {KeyEventsPlugin} from 'angular2/src/core/render/dom/events/key_events';
```

2.template中修改需要加入键盘事件的HTML元素，使用时该元素要先获得焦点
```
<div (keyup) ="onKeyDown($event)" tabindex="0">
```

3.class中加入以下方法，取得的lastKey为字符串
```
onKeyDown(event): void {
  this.lastKey = KeyEventsPlugin.getEventFullKey(event);
  event.preventDefault();
}
```

## 自定义事件
1.引入依赖
```
import {Component, View, EventEmitter} from 'angular2/angular2';
```

2.@Component声明
```
@Component({
    selector: 'zippy',
    events: ['open', 'close']
})
```

3.class类里定义事件变量
```
export class Zippy {
constructor() {
  this.open = new EventEmitter();
  this.close = new EventEmitter();}}
```

4.触发方法
toggle()方法执行，将触发事件：
```
toggle() {
      (this.visible)?this.open.next({src:’111’}):this.close.next();
    }
{src:’111’}为事件传参，在下面的$event会收到这个参数
```

5.使用该组件事件
```
<zippy (open)="sayOpen($event)" (close)="sayClose()"></zippy>
$event为事件传入参数
```
(open)可写为on-open，(close)可写为on-close

事件从组件内部发送到组件上，从而可以调用其它组件的方法：
```
<gadget-input (store)="gadget.onAddItem($event)"></gadget-input>
<gadget-list #gadget></gadget-list>
```

## Observer事件
1.引用依赖
```
import {ObservableComponent} from 'base/core/ObservableComponent';
import {Event} from 'base/core/Event';
```

2.定义一个类
重写listNotificationInterests，返回一个数组包括所有事件名
用Event.getInstance().on方法设置所有事件的回调函数
```
class MyEvent extends ObservableComponent{
  constructor(){
    super();
    super.onInit();
    Event.getInstance().on("aaa", () => { console.log("I'm aaa") });
    Event.getInstance().on("bbb", () => { console.log("I'm bbb") });
  }

  listNotificationInterests() {
    return ["aaa", "bbb"];
  }
}
```

3.生成一个实例
```
constructor(iptvService: IptvService) {
    this.MyEvent = new MyEvent();
}
```

4.调用函数发事件
```
emitTest(){
    Event.getInstance().emit("bbb");
    Event.getInstance().emit("aaa");
}
```

## Lifecycle
Lifecycle可以看作是组件自带的系统事件，在组件运行的关键时间点可添加处理函数，alpha.37改为如下写法请注意。
例：
1.import
```
import {OnInit, OnDestroy} from 'angular2/angular2';
```

2.重写相关Lifecycle方法
```
export class About implements OnInit, OnDestroy {
  onInit(){
    ...
  }

  onDestroy(){
    ...
  }
}
```