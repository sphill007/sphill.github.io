# docker拉取镜像超时，无法正常启动
## 问题
```
$ docker-compose up -d
Creating network "1224-rce_default" with the default driver
Pulling web (vulhub/fastjson:1.2.24)...
ERROR: Get https://registry-1.docker.io/v2/: net/http: request canceled (Client.Timeout exceeded while awaiting headers)
```

## 解决办法：修改镜像源为国内镜像源
```
$ sudo vim /etc/docker/daemon.json
```
写入自定义仓库
```
{
    "registry-mirrors":["https://docker.mirrors.ustc.edu.cn"]
}
```
然后重启docker
```
$ sudo systemctl daemon-reload
$ sudo systemctl restart docker
```
再执行docker-compose up即可正常拉取镜像并启动了
```
vagrant@ubuntu-budgie-18:~/vulhub/shiro/CVE-2016-4437$ docker-compose up -d
Pulling web (vulhub/shiro:1.2.4)...
1.2.4: Pulling from vulhub/shiro
43c265008fae: Already exists
af36d2c7a148: Already exists
2b7b4d10e1c1: Already exists
f264389d8f2f: Already exists
1a2c46e93f4a: Already exists
f9506bb322c0: Already exists
96f5dad14c2c: Already exists
b6ea9c6684a0: Pull complete
Creating cve-2016-4437_web_1 ... done
```

如果windows平台使用docker desktop，修复问题方法类似，直接修改docker desktop配置，添加镜像源为国内镜像源，apply and restart即可。
