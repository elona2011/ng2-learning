# inject
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

# 参考：
https://github.com/SekibOmazic/angular2-playground
http://blog.thoughtram.io/angular/2015/09/03/forward-references-in-angular-2.html