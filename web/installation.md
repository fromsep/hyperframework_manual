## 安装

---

### 1.手动初始化项目
按照 [入门](/web/getting_started.md) 文档提供的步骤初始化项目文件夹和文件。

### 2.通过脚手架初始化项目
Web 应用脚手架位于 Hyperframeowrk 项目的 skeletons/web 目录中。

website 文件夹包含网站应用脚手架，api 文件夹包含 API 应用脚手架。

### 3.配置 Web 服务器 URL 重写规则

- Nginx

```
server {
    listen 80;
    server_name localhost;
    root /website/public;

    location / {
        index index.php;
        try_files $uri $uri/ /index.php?$args;
    }

    location ~ ^/index.php$ {
        fastcgi_pass unix:/var/run/php5-fpm.sock;
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
        include fastcgi_params;
    }
}
```

- Apache

```
<VirtualHost localhost:80>
    ServerName   localhost
    DocumentRoot /website/public
    RewriteEngine Off

    <Location />
        RewriteEngine On
        RewriteCond %{REQUEST_FILENAME} -s [OR]
        RewriteCond %{REQUEST_FILENAME} -l [OR]
        RewriteCond %{REQUEST_FILENAME} -d
        RewriteRule ^.*$ - [NC,L]
        RewriteRule ^.*$ /index.php [NC,L]
    </Location>
</VirtualHost>
```