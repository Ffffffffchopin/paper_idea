
一开始一直不理解菜鸟教程和实用Linux手册上的教程，即
```shell
find path -option 
```

的基本格式，因为我在查找腾讯云中的Nginx位置时使用

```shell
find Nginx
```
和

```shell
find -name Nginx
```

似乎都能工作，不理解为什么可以直接搜索还要加-name的选项名，后来才理解

### 命令中第二位的是查找的根目录

正确的写法应该是

```shell
find / -name Nginx
```

```shell
(base) [root@VM-8-16-centos /]# find / -name nginx
/usr/local/nginx
/usr/local/nginx/sbin/nginx
/www/server/panel/vhost/template/nginx
/www/server/panel/vhost/nginx
/www/server/panel/rewrite/nginx
/var/lib/yum/repos/x86_64/7/nginx
/var/cache/yum/x86_64/7/nginx
/root/nginx-1.18.0/objs/nginx
/root/anaconda3/pkgs/notebook-6.4.8-py39h06a4308_0/lib/python3.9/site-packages/notebook/static/components/codemirror/mode/nginx
/root/anaconda3/lib/python3.9/site-packages/notebook/static/components/codemirror/mode/nginx
```


一下子便豁然开朗了不少

另附一些常用的命令参数



