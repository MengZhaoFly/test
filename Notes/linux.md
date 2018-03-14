## PATH
和windows配置环境变量一样，执行命令的时候也会从path里面一一查找。
nginx path: /usr/local/nginx/sbin/
1. 立即生效,临时改变,当前用户 `$PATH` 是一个变量
```bash
export PATH=/usr/local/nginx/sbin/:$PATH
```
2. source刷新，永久生效，当前用户
```bash
vim ~/.bashrc 
//在最后一行添上：
export PATH=/usr/local/nginx/sbin/:$PATH
```
3. 系统重启，永久生效，所有用户
```bash
vim /etc/profile
/export PATH //找到设置PATH的行，添加
export PATH=/usr/local/nginx/sbin/:$PATH
```
