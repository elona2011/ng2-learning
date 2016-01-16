2	import,export
import引入依赖的模块及自定义组件
例1：``import {ComponentMetadata as Component, ViewMetadata as View, bootstrap, CORE_DIRECTIVES } from 'angular2/angular2';``
例2：``import {Zippy} from 'zippy';``

export输出组件和函数
例1：``export class Search {}``
例2：``export function status(response) {...}``

2.1	依赖关系
FORM_DIRECTIVES:ng-model
ROUTER_DIRECTIVES:<router-outlet>
CORE_DIRECTIVES:NgIf, NgFor, Pipe, OnInit		包含所有CORE里的指令
例1：
```
import {Component, View, CORE_DIRECTIVES, NgStyle} from 'angular2/angular2';
@View({
	directives: [CORE_DIRECTIVES, NgStyle]
})
```
例2：
```
import {Component, View, EventEmitter} from 'angular2/angular2';
import {FORM_DIRECTIVES} from 'angular2/forms';
import { RouterOutlet } from 'angular2/router';
import { RouterLink } from 'angular2/router';
import { ROUTER_DIRECTIVES, RouteConfig } from 'angular2/router';
import { ROUTER_BINDINGS, LocationStrategy, HashLocationStrategy } from 'angular2/router';
```
