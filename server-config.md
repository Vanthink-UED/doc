
#服务器配置说明

<b>一般服务器配置放在config/目录下.</b>

请自行按照域名配置规范进行配置文件比如:

用户姓名＋项目姓名 ＋ vanthink.cn

比如:jack.online.vanthink.cn

配置apache或者nginx请自行加软链接或者在配置中写明

```shell
cd /usr/local/nginx  进入服务器配置目录
ln -s /repos/product/config/xxxx.conf xxxx.conf  建立软链接
service apachetcl | nginx restart  重启服务

```
随后在本地hosts文件修改成层 127.0.0.1 xxxx.vanthink.cn

如果存在服务中转,即server 层会进行服务的请求和分发，需要在server配置中hosts

``` shell
vim /etc/hosts

```

撰写vhost可以参考 http://blog.csdn.net/justflyhigh/article/details/7611741

```apache
<VirtualHost *:80>
    ServerAdmin webmaster@dummy-host2.example.com
    ; 更目录
    DocumentRoot "/Applications/XAMPP/xamppfiles/htdocs/vanthink"
    ;域名
    ServerName user.product.vanthink.cn  
    ; 目录配置 重写规则等
    <Directory "/home/dev/www/dev/product">
        Options +Includes -Indexes
        AllowOverride All
        Order Deny,Allow
        Allow from All
    </Directory>
    ; 日志目录
    ErrorLog "/Applications/XAMPP/xamppfiles/logs/user.product.vanthink.cn-error_log"
    CustomLog "/Applications/XAMPP/xamppfiles/logs/user.product.vanthink.cn-access_log" common
</VirtualHost>


```

```nginx
server {
        listen       80;
        server_name user.product.vanthink.cn;
        root  /home/www/api.vanthink.cn;
        if (!-e $request_filename) {
                rewrite ^/(.*) /public/index.php?$1 last;
        }
        index /public/index.php;

        location ~ .*\.(php|php5)?$ {
                fastcgi_pass 127.0.0.1:9000;
                fastcgi_index index.php;
                fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
                include fastcgi_params;
                client_max_body_size  20m;
        }
}

```


#### 参考

1. [apache]: http://www.uow.edu.au/~nabg/WebServer/Chapter3/WindowsConf.html

2. [nginx]: https://www.nginx.com/resources/wiki/start/topics/examples/full/
