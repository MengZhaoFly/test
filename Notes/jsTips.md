> ## [About jstips](http://www.jstips.co/)
![](http://www.jstips.co/assets/images/jstips-animation.gif)
官方介绍 __每天一条JS小知识!__ 可是每天打开感觉就没变过，不知道是不是前面的flag立得太早。😂
1. js object (purely for storing data), without side effects.
   纯粹用一个对象存储数据的时候，可以用
   ```js
   const map = Object.create(null);
   ```
   创建一个对象，
   好处：
   `for in`遍历的时候不用每次`hasOwnProperty`过滤原型上的属性，因为它甚至没有`hasOwnProperty, constructor, toString`方法.
2. DOM event listening
   不再需要的时候，最好对绑定的事件解除。
3. Array Hacks；
   - 调用一个函数某些参数不是必要的传`null undefined`总是怪的
   ```
   foo(...['parameter1', , 'parameter3'])
   ```
4. `key`这个属性
> Key is not really about performance, it’s more about identity (which in turn leads to better performance). Randomly assigned and changing values do not form an identity [Paul O’Shannessy](https://github.com/facebook/react/issues/1342#issuecomment-39230939)<br/>
```html
<ul>
   <li key={Math.random()}></li>
   <li></li>
</ul>
```
这是很傻的做法，每次都是重建所有的孩子，因为key不能代表每个元素的身份 每次都不同。
