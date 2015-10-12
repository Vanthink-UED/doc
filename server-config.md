
#服务器配置说明

请自行按照域名配置规范进行配置文件比如:

用户姓名＋项目姓名 ＋ vanthink.cn

比如:puhuan.online.vanthink.cn or zhengganyun.cdn.vanthink.cn

配置apache或者nginx请自行加软链接或者在配置中说明

随后在本地hosts文件修改成层 127.0.0.1 xxxx.vanthink.cn

撰写vhost可以参考 http://blog.csdn.net/justflyhigh/article/details/7611741

```apache
<VirtualHost *:80>
    ServerAdmin webmaster@dummy-host2.example.com
    ; 更目录
    DocumentRoot "/Applications/XAMPP/xamppfiles/htdocs/vanthink"
    ;域名
    ServerName puhuan.online.vanthink.cn  
    ; 目录配置 重写规则等
    <Directory "/Applications/XAMPP/xamppfiles/htdocs/vanthink">
        Options +Includes -Indexes
        AllowOverride All
        Order Deny,Allow
        Allow from All
    </Directory>
    ; 日志目录
    ErrorLog "/Applications/XAMPP/xamppfiles/logs/puhuan.online.vanthink.cn-error_log"
    CustomLog "/Applications/XAMPP/xamppfiles/logs/puhuan.online.vanthink.cn-access_log" common
</VirtualHost>


```

```nginx



```
