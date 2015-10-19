#svn 以及 git 项目规范

###目录设置

``` javascript

+ project/
|   + trunk
|   + tags
|       + release_0.1
|   + branches

```


###项目切出

```shell

svn co https:svn.vanthink.cn/project/branches/pro1.1 branche_pro1.1
unlink pro
ln -s branche_pro1.1 pro
```