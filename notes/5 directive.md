# @Directive
https://github.com/angular/angular/blob/master/modules/angular2/docs/core/02_directives.md

# 常用指令
## #
定义一个当前组件的局部变量，绑定当前位置的HTML元素，变量名只能小写
例1：``<input #searchvalue (keyup)="searchArtist(searchvalue.value)"/>``
例2：``<input class="form-control" type="text" placeholder="Your new friend" #friend (keyup) ="update(friend.value)">``

## \\{\\{\\}\\}

动态变量或表达式
```
例1：``{{i%6}}``
例2：``<div>{{visible?'&blacktriangledown;':'&blacktriangleright;'}}</div>``
```
## ``[]``
[参数]用于父组件向子组件传递参数，(事件)用于子组件向父组件传递事件。
例：``<todo-cmp [model]="todo" (complete)="onCompletingTodo(todo)"></todo-cmp>`` 其中model是子组件中定义的参数，todo是父组件中的变量，如果todo改变，model也会自动改变；complete是子组件中定义的事件，onCompletingTodo是父组件中的方法，complete事件将触发onCompletingTodo方法。

## ng-for
例：``<div *ng-for="#content of contentList; #i= index">``
contentList为将遍历的数组，#content为遍历数组的元素，#i为数组指针。在当前div及其子元素可用``{{content}}``和``{{i}}``进行引用
## ng-if
当*ng-if之后的表达式为true，则显示该HTML元素；反之则删除。显示删除过程会触发Lifecycle
例：
```
<div>
  <btv-player-menu *ng-if="isShowBtvPlayerMenu"></btv-player-menu>
  <btv-player-minidetail-page *ng-if="isShowBtvPlayerMinidetailPage"></btv-player-minidetail-page>
  <btv-player-reminder *ng-if="isShowBtvPlayerReminder"></btv-player-reminder>
</div>
```

## ng-switch

## ng-model

## ng-style
例1：``<div [ng-style]="{'background-image':'url('+picture+')'}"></div>`` 背景图绑定picture变量，picture为图片地址
例2：``<div [ng-style]="{'text-align': alignExp}"></div>``
例3：``<div [ng-style]="styleExp"></div>``  可以是变量

## ng-class
根据表达式的结果添加或移除CSS属性
例：``<div class="button" [ng-class]="{active: isOn, disabled: isDisabled}">``

##  ng-content
``<ng-content></ng-content>``表明其它组件或内容插入当前组件的位置。
例：``<zippy><p>111</p></zippy>``，其中``<p>111</p>``将插入zippy组件的template中的ng-content位置。

##  router-outlet
router的输出位置。

##  router-link
router-link表示跳转名称为search的地址，而不是跳转到/search的url下，见@RouteConfig。
有三种写法：
例1：``[router-link]="['./search']"`` search位于当前组件路径下
例2：``[router-link]="['../search']"``  search位于当前组件的父路径下
例3：``[router-link]="['/search']"``  绝对路径，从根路径开始
还可以传递参数：
例4：``[router-link] =”['/team', {teamId: 1}, 'user', {userId: 2}]”``


##  Pipe
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

# 参考：
http://www.shmck.com/angular-2-pipes/
https://github.com/auth0/angular2-pipes