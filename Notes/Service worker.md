## what
Service worker是注册在指定源和路径下的驱动worker。
浏览器和应用程序／浏览器和服务器 之间的代理。
1. 相对于驱动应用的js来说，运行在另外一个线程中，不会造成阻塞，不能访问DOM，完全是异步的设计。
2. 只能有https承载
## 生命周期
1. 完全独立于web页面。
2. 要想生效必须注册，注册之后浏览器会启动一个安装service work的过程。
3. 安装过程中浏览器会缓存一些静态资源，如果有文件缓存失败，那么就service work不会被激活。
4. 如果已有service work激活则该service work安装后不会被激活处于waiting状态，直到所有页面不再使用才会被激活。
5. service work激活后便会接管页面，如果一个页面首次激活则会在下次被接管。
6. 缓存的资源被fetch时都会触发fetch事件。
## api
`waitUntil`:确保里面的代码执行完毕service work才会被安装.   
`addALl`:缓存所有的资源

