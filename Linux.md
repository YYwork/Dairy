# Linux 命令

[JS Linux](http://bellard.org/jslinux/)

linux中的每个用户必须属于一个组。
每个文件有所有者、所在组、其它组的概念。
除开文件的所有者和所在组的用户外，系统的其它用户都是文件的其它组。



用`ls ‐ahl`命令可以看到文件的所有者。

`chown` (change owner)
`chgrp` (change group)

`ls -l`
 
 ```
 lrwxrwxrwx    1 root     root             9 Mar  8 05:22 dos -> /root/dos       
-rw-r--r--    1 root     root           242 Mar  8 05:22 hello.c 
 ```
- 10个字符确定不同用户能对文件干什么
- 第一个字符代表文件（-）、目录（d），链接（l）
- 其余字符每3个一组（rwx），读（r）、写（w）、执行（x）
- 第一组rwx：文件所有者的权限是读、写和执行
- 第二组rw-：与文件所有者同一组的用户的权限是读、写但不能执行
- 第三组r--：不与文件所有者同组的其他用户的权限是读不能写和执行

也可用数字表示为：r=4，w=2，x=1  因此rwx=4+2+1=7

- 1 表示连接的文件数
- root 表示用户
- root表示用户所在的组
- 1213 表示文件大小（字节）
- Feb 2 09:39 表示最后修改日期
- abc 表示文件名

`chmod` 改变文件或目录的权限

`chmod 755 abc`：赋予abc权限`rwxr-xr-x`
`chmod 644 abc.js`：赋予abc.js权限`rw-r--r--`
`chmod u=rwx，g=rx，o=rx abc`：同上u=用户权限，g=组权限，o=不同组其他用户权限
`chmod u-x，g+w abc`：给abc去除用户执行的权限，增加组写的权限
`chmod a+r abc`：给所有用户添加读的权限

