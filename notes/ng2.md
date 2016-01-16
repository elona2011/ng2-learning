


5 @Directive
https://github.com/angular/angular/blob/master/modules/angular2/docs/core/02_directives.md

6 常用指令
6.1 #
定义一个当前组件的局部变量，绑定当前位置的HTML元素，变量名只能小写
例1：``<input #searchvalue (keyup)="searchArtist(searchvalue.value)"/>``
例2：``<input class="form-control" type="text" placeholder="Your new friend" #friend (keyup) ="update(friend.value)">``

6.2 \\{\\{\\}\\}

动态变量或表达式
```
例1：``{{i%6}}``
例2：``<div>{{visible?'&blacktriangledown;':'&blacktriangleright;'}}</div>``
```
6.3 ``[]``
[参数]用于父组件向子组件传递参数，(事件)用于子组件向父组件传递事件。
例：``<todo-cmp [model]="todo" (complete)="onCompletingTodo(todo)"></todo-cmp>`` 其中model是子组件中定义的参数，todo是父组件中的变量，如果todo改变，model也会自动改变；complete是子组件中定义的事件，onCompletingTodo是父组件中的方法，complete事件将触发onCompletingTodo方法。

6.4 ng-for
例：``<div *ng-for="#content of contentList; #i= index">``
contentList为将遍历的数组，#content为遍历数组的元素，#i为数组指针。在当前div及其子元素可用``{{content}}``和``{{i}}``进行引用
6.5 ng-if
当*ng-if之后的表达式为true，则显示该HTML元素；反之则删除。显示删除过程会触发Lifecycle
例：
```
<div>
  <btv-player-menu *ng-if="isShowBtvPlayerMenu"></btv-player-menu>
  <btv-player-minidetail-page *ng-if="isShowBtvPlayerMinidetailPage"></btv-player-minidetail-page>
  <btv-player-reminder *ng-if="isShowBtvPlayerReminder"></btv-player-reminder>
</div>
```

6.6 ng-switch

6.7 ng-model

6.8 ng-style
例1：``<div [ng-style]="{'background-image':'url('+picture+')'}"></div>`` 背景图绑定picture变量，picture为图片地址
例2：``<div [ng-style]="{'text-align': alignExp}"></div>``
例3：``<div [ng-style]="styleExp"></div>``  可以是变量

6.9 ng-class
根据表达式的结果添加或移除CSS属性
例：``<div class="button" [ng-class]="{active: isOn, disabled: isDisabled}">``

6.10  ng-content
``<ng-content></ng-content>``表明其它组件或内容插入当前组件的位置。
例：``<zippy><p>111</p></zippy>``，其中``<p>111</p>``将插入zippy组件的template中的ng-content位置。

6.11  router-outlet
router的输出位置。

6.12  router-link
router-link表示跳转名称为search的地址，而不是跳转到/search的url下，见@RouteConfig。
有三种写法：
例1：``[router-link]="['./search']"`` search位于当前组件路径下
例2：``[router-link]="['../search']"``  search位于当前组件的父路径下
例3：``[router-link]="['/search']"``  绝对路径，从根路径开始
还可以传递参数：
例4：``[router-link] =”['/team', {teamId: 1}, 'user', {userId: 2}]”``


6.13  Pipe
1.import
```
import {Pipe} from 'angular2/angular2';
```

2.根据Pipe设定变量类型
```
public starttime: number = 0;
public endtime: number = 0;
this.starttime = parseInt(this.playbilllist.playbilllist[0].startTimeMilli);
this.endtime = parseInt(this.playbilllist.playbilllist[0].endTimeMilli);
```

3.使用Pipe设定时间
```
<div>{{starttime | date:'HHmm'}} - {{endtime | date:'HHmm'}}</div>
```
参考：
http://www.shmck.com/angular-2-pipes/
https://github.com/auth0/angular2-pipes

7 bootstrap
启动Main程序，[]中的绑定将全局可用
例：bootstrap(App, []);
8 inject
1.template中，注入的类为父子关系
```
<pet-list >
<pet-input></pet-input>
</pet-list>
```

2.import
```
import {PetList} from 'byinjection/PetList';
import { Inject, forwardRef} from 'angular2/angular2'; 
```

3.class注入，调用注入class的方法
```
export class PetInput {
  petList: PetList;

  constructor(@Inject(forwardRef(()=>PetList)) petList:PetList) { //petList为单例，指向dom树中的<pet-list>
    this.petList = petList;
  }

  doSomeThing(){
  this.petList.addItem(...); //调用petList的方法，可以传参
}
}
```

参考：
https://github.com/SekibOmazic/angular2-playground
http://blog.thoughtram.io/angular/2015/09/03/forward-references-in-angular-2.html

9 事件
9.1 系统事件
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

9.2 自定义事件
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

9.3 Observer事件
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

9.4 Lifecycle
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

10  Router
10.1  router策略
``bind(LocationStrategy).toClass(HashLocationStrategy)`` 使用hash url定位策略
``bind(LocationStrategy).toClass(PathLocationStrategy)`` 需在index.html的<head>中加入<base href="/">

10.2  @RouteConfig
```
@RouteConfig([
  { path: '/', redirectTo: '/search' },
  { path: '/search', as: 'search', component: Search },
  { path: '/artist/:id', as: 'artist', component: Artist }
])
```
path: '/'为默认路径。
redirectTo：跳转到其它路径
as：路径的别名，用于[router-link]中引用
component：引用的组件类名

10.3  router设置
```
1.import { ROUTER_BINDINGS, LocationStrategy, HashLocationStrategy, PathLocationStrategy } from 'angular2/router';
import {bind} from 'angular2/angular2';
import { ROUTER_DIRECTIVES, RouteConfig, RouterLink } from 'angular2/router';
bootstrap(App, [ROUTER-BINDINGS, bind(LocationStrategy).toClass(HashLocationStrategy)]);

2.@RouteConfig([
    {path:'/', component:Start, as: 'start'}
])
3.<router-outlet></router-outlet>
directives: [ROUTER_DIRECTIVES, RouterLink]

4.<a [router-link]="['./user']">link to user component</a>
```

10.4  router跳转
1.import
```
import {Router} from 'angular2/router';
```

2.constructor注入
```
constructor(..., public router: Router) {
    ...
  }
```

3. url跳转方法
```
this.router.navigateByUrl('/home/livetv');
```

10.5  父子路由
1、  针对父—子路由：
父路由配置（在父ts文件下）：
  （1）、导入路由所需组件：
```
import { Router, RouteConfig, ROUTER_DIRECTIVES, ROUTER_BINDINGS } from 'angular2/router';
```
  （2）、配置路由：
```
@RouteConfig([
  { path: '/', redirectTo: '/login/userlogin' },   // redirectTo默认页面
  { path: '/login/...', component: Login, as: 'login' },  // component为导入的组件
  { path: '/mytvNavigation/...', component: MyTVNavigation, as: 'mytvNavigation' }
])
```
子路由配置（子ts文件中）：
  （1）、同上；
  （2）、配置路由：
```
@RouteConfig([
  { path: '/mytvNavigation', redirectTo: '/history'},
  { path: '/history', component: History, as: 'history'},
  { path: '/favorite', component: Favorite, as: 'favorite' },
{ path: '/profile/...', component: Profile, as: 'profile'}
])
```

其中path最好写上父路由路径，如果不写，在页面跳转时要加上父路径的path。
如果子路由下还存在子路由（如profile），以此类推……
注：凡是配置路由的ts文件，其``@View{}``中必须配置路由出口``<router-outlet></router-outlet>``，否则即使url地址变化，页面内容还是显示不出或者跳转不了！！！！
路由出口需要的组件：ROUTER_DIRECTIVES / RouterOutlet

11  Service服务
service是单例，数据共享给所有使用者
11.1  自定义Service
使用服务的4步，包括定义、引入、绑定、使用
1.定义Service
在angular2中，服务就是一个类。例：自定义一个简单的服务：
```
export class DataService {
  items:Array<any>;

  constructor() {
    this.items = [
      { name: 'Christoph Burgdorf' },
      { name: 'Pascal Precht' },
      { name: 'thoughtram' }
    ];
  }

  getItems() {
    return this.items;
  }
};
```
2.引入Service
```
import {DataService} from 'dataService';
```
