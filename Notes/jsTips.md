> ## [About jstips](http://www.jstips.co/)
![](http://www.jstips.co/assets/images/jstips-animation.gif)
官方介绍 __每天一条JS小知识!__ 可是每天打开感觉就没变过，不知道是不是前面的flag立得太早。😂
* js object (purely for storing data), without side effects.
  纯粹用一个对象存储数据的时候，可以用
  ```js
  const map = Object.create(null);
  ```
  创建一个对象，
  好处：
  `for in`遍历的时候不用每次`hasOwnProperty`过滤原型上的属性，因为它甚至没有`hasOwnProperty, constructor, toString`方法.
