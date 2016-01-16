# @View视图
## directives
template中用到的angular指令和自定义指令，camel驼峰写法。
例：``directives: [EzCard],``

## template
该视图的模板，html代码。directives要用小写中划线写法。
例：``template: ‘< ez-card [title1]="'deeeeeeee'"></ ez-card >’,``

HTML元素属性的几种写法：
``title="Details"``：title属性为字符串Details
``[title]="'Details'"``： title属性为字符串Details
``[title]="Details"``： title属性为变量Details
``bind-title=”’Details’”``： title属性为字符串Details

 ``<input #searchvalue (keyup)="searchArtist($event, searchvalue.value)"/>`` #searchvalue会双向绑定到input对象上，searchvalue.value可实时更新input输入值

## templateUrl
模板地址，引入外部HTML文件。例：``templateUrl: 'zippy.html'``

## styles
``styles: ['.tabs1 {background-color: green;}','{...}'],`` 声明的样式只在本组件中可用，默认，取决于encapsulation

## styleUrls
``styleUrls: ['zippy.css'],`` 声明外部样式文件
此外还可以直接写在template中，多用于关联动态样式，如生成动态获取的背景图片

下面有导致hexo出错的BUG

## encapsulation
封装设置。
ViewEncapsulation.None 无样式封装，样式位于<head>中，将全局可用。
ViewEncapsulation.Emulated 样式模拟，样式位于<head>中，仅当前组件可用，默认。
ViewEncapsulation.Native 当前组件可用，样式位于组件中，仅当前组件可用。