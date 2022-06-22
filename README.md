# clash-ubuntu-config

# 【Clash科学上网】ubuntu 22.04 配置使用 clash for linux

## 环境

系统：Ubuntu 22.04 LTS
软件：clash v1.11.0

## 下载、安装 clash for Linux

github 地址：https://github.com/Dreamacro/clash
下载最新版本 clash：https://github.com/Dreamacro/clash/releases

或者直接通过 wget 下载：

```
wget -O clash.gz https://github.com/Dreamacro/clash/releases/download/v0.0.0/clash-linux-amd64-v0.0.0.gz
```

解压到当前文件夹下：

```
gzip -f clash.gz -d
```

授权可执行权限：

```
chmod +x clash
```

初始化执行 clash：

```
./clash -d .
```

初始化执行 clash 会默认在当前目录下生成配置文件和全球IP地址库：  config.yaml和Country.mmdb

一般不会下载失败，只下载 Country.mmdb 就可以了，配置文件替换成自己的

配置 clash
clash 使用 yaml 作为配置文件，配置文件示例可以参考 github 上的文档或我们使用自己的配置（机场一般都会给），并将名称改为 config.yaml

再次执行 clash：

```
./clash -d .
```

## 开机自启

在终端里执行

```
vim /etc/systemd/system/clash.service
```

填入


```
[Unit]
Description=Clash Service
After=network.target

[Service]
ExecStart=/home/user/clash/clash -d /home/user/clash/
ExecStop=/bin/kill $MAINPID
[Install]
WantedBy=multi-user.target
```

开机启动
```
sudo systemctl enable clash.service
```

## web dashboard

我找到的 clash for linux 的版本是不带控制界面的，需要访问 [这个 web 控制台](http://clash.razord.top/#/proxies) 才能进行控制。后来为了方便访问，我就把他的包都给抓了下来，放在了本地的 nginx 上。
 https://github.com/muzihuaner/web-dashboard-for-clash-with-nginx

https://clash.quickso.cn

## 配置 Ubuntu 代理

打开 设置 -> 网络 -> 网络代理
配置 HTTP、HTTPS、Socket 代理

代理方式：手动

http 127.0.0.1:7890
https 127.0.0.1:7890
socks 127.0.0.1:7891

## 验证

打开
https://www.google.com.hk
如果正常打开就没有问题啦！

