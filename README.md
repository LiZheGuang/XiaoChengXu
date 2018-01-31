**小程序开发中的小技巧**

>总结出来的一些技巧，其实也在文档里面，但是略有偏差并且不容易被搜到；

### 怎么拿到小程序当前页的路径地址？

	 1.this.route 在页面内的JS文件内就可以拿到当前的路径地址
	 
	 2.也可以在APP.js里面拿去到页面的地址 onLaunch,onShow的回调里path为小程序的路径地址

###	怎么获取到App.js里面的公用变量?
	
	很简单 假设在index.js里要拿取App.js里的某个变量需要写 getApp().xxx 

	全局的 getApp() 函数可以用来获取到小程序实例

	但是如果你要在App.js里面拿取他内部的某个实例 直接this.xxx即可

	注意：通过 getApp() 获取实例之后，不要私自调用生命周期函数。

### 什么是场景值？怎么获取场景值？
	
	场景值:用户以什么样的渠道进入到小程序 微信都会定义为某个编号的场景值。 比如 1012 场景值为长按图片识别二维码的场景值

	获取场景值:可以在 App 的 onlaunch 和 onshow 中获取上述场景值 同样为 这两个生命周期回调函数内的 scene 


### 学会使用wx:key
	
	官方文档中这样说:如果列表中项目的位置会动态改变或者有新的项目添加到列表中，并且希望列表中的项目保持自己的特征和状态（如 <input/> 中的输入内容，<switch/> 的选中状态），需要使用 wx:key 来指定列表中项目的唯一的标识符。

	wx:key 的值以两种形式提供

	字符串，代表在 for 循环的 array 中 item 的某个 property，该 property 的值需要是列表中唯一的字符串或数字，且不能动态改变。
	保留关键字 *this 代表在 for 循环中的 item 本身，这种表示需要 item 本身是一个唯一的字符串或者数字，如：
	当数据改变触发渲染层重新渲染的时候，会校正带有 key 的组件，框架会确保他们被重新排序，而不是重新创建，以确保使组件保持自身的状态，并且提高列表渲染时的效率。

	如不提供 wx:key，会报一个 warning， 如果明确知道该列表是静态，或者不必关注其顺序，可以选择忽略


```
<switch wx:for="{{objectArray}}" wx:key="unique" style="display: block;"> {{item.id}} </switch>
<button bindtap="switch"> Switch </button>
<button bindtap="addToFront"> Add to the front </button>

<switch wx:for="{{numberArray}}" wx:key="*this" style="display: block;"> {{item}} </switch>
<button bindtap="addNumberToFront"> Add to the front </button>
```

### 模板传参的方法

```
var Json = {
	A:1
}

<template is="xxx" data="{{...json}}"/>

也可以这样

<template is="xxx" data="{{obj:Json}}"/>

```












