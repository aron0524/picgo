# Hyperf3
## Nginx配置



```php

upstream hyperf {
    # Hyperf HTTP Server 的 IP 及 端口
    server 127.0.0.1:9501;
    #server 127.0.0.1:9502;
}
server
{
    listen 80;
    # listen 9501;
    server_name hyperf3.test;
    #autoindex on;
    index index.php index.html index.htm default.php default.htm default.html;
    root /www/wwwroot/hyperf3.test;

    #SSL-START SSL相关配置，请勿删除或修改下一行带注释的404规则
    #error_page 404/404.html;
    #SSL-END

    #ERROR-PAGE-START  错误页配置，可以注释、删除或修改
    #error_page 404 /404.html;
    #error_page 502 /502.html;
    #ERROR-PAGE-END

    #PHP-INFO-START  PHP引用配置，可以注释或修改
    include enable-php-80.conf;
    #PHP-INFO-END

    #REWRITE-START URL重写规则引用,修改后将导致面板设置的伪静态规则失效
    include /www/server/panel/vhost/rewrite/hyperf3.test.conf;
    #REWRITE-END

    #禁止访问的文件或目录
    location ~ ^/(\.user.ini|\.htaccess|\.git|\.env|\.svn|\.project|LICENSE|README.md)
    {
        return 404;
    }

    #一键申请SSL证书验证目录相关设置
    location ~ \.well-known{
        allow all;
    }

    #禁止在证书验证目录放入敏感文件
    if ( $uri ~ "^/\.well-known/.*\.(php|jsp|py|js|css|lua|ts|go|zip|tar\.gz|rar|7z|sql|bak)$" ) {
        return 403;
    }

    # location ~ .*\.(gif|jpg|jpeg|png|bmp|swf)$
    # {
    #     expires      30d;
    #     error_log /dev/null;
    #     access_log /dev/null;
    # }

    # location ~ .*\.(js|css)?$
    # {
    #     expires      12h;
    #     error_log /dev/null;
    #     access_log /dev/null;
    # }
    location / {
        # 将客户端的 Host 和 IP 信息一并转发到对应节点  
        proxy_set_header Host $http_host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        add_header Access-Control-Allow-Methods 'GET, POST, OPTIONS';
        # 转发Cookie，设置 SameSite
        proxy_cookie_path / "/; secure; HttpOnly; SameSite=strict";
        # 执行代理访问真实服务器
        proxy_pass http://hyperf;
    }
    location /apidoc/{
        # proxy_next_upstream http_502 http_504 error timeout invalid_header;  
        # proxy_pass http://127.0.0.1:9501;  
        # proxy_set_header Host 127.0.0.1;  
        # proxy_set_header X-Forwarded-For $remote_addr;  
        # break;
        root "/www/wwwroot/hyperf3.test/public/";
        break;
    }
    location /static/{
        root "/www/wwwroot/hyperf3.test/public/";
        break;
    }

    access_log  /www/wwwlogs/hyperf3.test.log;
    error_log  /www/wwwlogs/hyperf3.test.error.log;
}

```



# [Docker Swarm 集群搭建](https://www.hyperf.wiki/3.0/#/zh-cn/tutorial/docker-swarm?id=docker-swarm-集群搭建)



sudo docker run -d --hostname gitlab.test \
--publish 4443:443 --publish 8080:80 --publish 22:22 \
--name gitlab --restart always --volume /srv/gitlab/config:/etc/gitlab \
--volume /srv/gitlab/logs:/var/log/gitlab \
--volume /srv/gitlab/data:/var/opt/gitlab \
--privileged=true \
gitlab/gitlab-ce:latest



##修改root密码

sudo docker exec -it 容器ID /bin/bash 
gitlab-rails console -e production


user.password = 'admin0524'
user.password_confirmation = 'admin0524'
user.save!

##修改配置文件
/srv/gitlab/config/gitlab.rb


postgresql['shared_buffers'] = "64MB"
postgresql['max_worker_processes'] = 1
sidekiq['concurrency'] = 1
nginx['worker_processes'] = 2
prometheus_monitoring['enable'] = false
prometheus['enable'] = false
prometheus_monitoring['enable'] = false
alertmanager['enable'] = false
node_exporter['enable'] = false
redis_exporter['enable'] = false
postgres_exporter['enable'] = false
pgbouncer_exporter['enable'] = false
gitlab_exporter['enable'] = false
grafana['enable'] = false
sidekiq['metrics_enabled'] = false
gitlab_rails['gitlab_default_projects_features_container_registry'] = false
gitlab_rails['registry_enabled'] = false
registry['enable'] = false
registry_nginx['enable'] = false
gitlab_rails['packages_enabled'] = false
gitlab_rails['dependency_proxy_enabled'] = false
gitlab_pages['enable'] = false
pages_nginx['enable'] = false
gitlab_rails['usage_ping_enabled'] = false
gitlab_rails['sentry_enabled'] = false
grafana['reporting_enabled'] = false
gitlab_kas['enable'] = false
gitlab_rails['gitlab_kas_enabled'] = false
gitlab_rails['terraform_state_enabled'] = false
gitlab_rails['kerberos_enabled'] = false
sentinel['enable'] = false
mattermost['enable'] = false
mattermost_nginx['enable'] = false
puma['worker_processes'] = 0
puma['min_threads'] = 1
puma['max_threads'] = 2
sidekiq['max_concurrency'] = 5
gitlab_rails['smtp_enable'] = false
gitlab_rails['gitlab_email_enabled'] = false
gitlab_rails['incoming_email_enabled'] = false
gitlab_ci['gitlab_ci_all_broken_builds'] = false
gitlab_ci['gitlab_ci_add_pusher'] = false



##重启
docker exec gitlab gitlab-ctl reconfigure








**文档属性**

-------------------------------------------------------
  属性            	内容

  作者            	aron0524

  文档标题        数据填充工具Faker

  文档版本        1.0

  文档日期        2023-01-04
                  
------------------------------- ---------------------------------------

**文档版本信息**

----------- --------------------------------- --------------- -----------
  版本        修订日期                          修订人          描述

  1.0         2023年01月04日                   aron0524            初稿

----------- --------------------------------- --------------- -----------