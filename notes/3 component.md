# @Component组件

##	selector
组件名称。
例：``selector: 'zippy',``
##	properties
申明组件的外部属性,其它组件可以通过这个属性传入参数。
例1：``properties:['myTitle1',’myTitle2’]``
例2：``<zippy [my-title1]="title2"></zippy>`` 绑定title2变量
例3：``<zippy [my-title2] = "’title2’"></zippy>`` 绑定title2字符串
例4：``['tabTitle: tab-title']``申明变量tabTitle,将tab-title绑定到组件内的tabTitle变量上。内部绑定的优先级高于外部绑定，例如例4的绑定高于例2的绑定。
##	events
申明事件。
例：``events: ['open', 'close'],``

## host
内部事件。
例1：
```
host: {
    '(mouseenter)': 'focusElement("77")'
  }
```
例2：内部绑定和外部绑定的相互切换。一个属性同时在template和组件class中绑定，只要有其中一个值改变，属性值就会刷新。
```
import {View, Component, bootstrap, Directive, Host, Optional} from 'angular2/angular2'

@Component({
  selector: 'bank-account',
  properties: ['bankName:bank-name', 'id: account-id'],
  host: {
    '(mouseout)': 'focusElement("77")'
  }
})
@View({
  template: `
    Bank Name: {{bankName}}
    Account Id: {{id}}
  `
})
class BankAccount {
  bankName: string;
  id: string;
  
  constructor(){
    this.bankName = "222";
  }
  focusElement(isFocus) {
    this.bankName = isFocus;
  }
  
  // this property is not bound, and won't be automatically updated by Angular
  normalizedBankName: string;
}
@Component({selector: 'app'})
@View({
  template: `
    <bank-account [bank-name]="RBC1" account-id="4747" (click)="onclick()"></bank-account>
  `,
  directives: [BankAccount]
})
class App {
  RBC1: string;
  constructor(){
    this.RBC1 = "2221";
  }
  onclick(){
    this.RBC1 = this.RBC1+1;
  }
}
bootstrap(App);
```

## bindings
绑定依赖，先要import该依赖。绑定可供子模块查询。
例：``bindings: [IptvService, AuthenticateService]``

## viewBindings
``viewBindings:[bind(VideoService).toClass(SpecificVideoService)]``  绑定的对象只能供本模块使用，不会影响到子模块
