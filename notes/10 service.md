#  Service服务
service是单例，数据共享给所有使用者
##  自定义Service
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
