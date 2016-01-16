#  Router
##  router策略
``bind(LocationStrategy).toClass(HashLocationStrategy)`` 使用hash url定位策略
``bind(LocationStrategy).toClass(PathLocationStrategy)`` 需在index.html的<head>中加入<base href="/">

##  @RouteConfig
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

## router设置
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

##  router跳转
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

##  父子路由
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
