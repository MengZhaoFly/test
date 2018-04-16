## require('module')
`module` node原生的模块
```js
const nativeModule = require('module');
const vm = require('vm');
const wrapper = nativeModule.wrap(moduleString);
//为什么我们可以在代码里用require/module (function(exports, require, module, __filename, __dirname) {code here})()
const m = {exports: {}}
const script = new vm.Script(wrapper, {
fileName: 'filename',
displayError: true
})
const result = script.runInthisContext();
result.call(m.exports, m.exports, require, m)
return m;
```
