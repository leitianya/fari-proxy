# fari-proxy

[![Build Status](https://travis-ci.org/Leviathan1995/fari-proxy.svg?branch=master)](https://travis-ci.org/Leviathan1995/fari-proxy)
[![Go Report Card](https://goreportcard.com/badge/github.com/leviathan1995/fari-proxy)](https://goreportcard.com/report/github.com/leviathan1995/fari-proxy)
[![GitHub version](https://badge.fury.io/gh/leviathan1995%2Ffari-proxy.svg)](https://badge.fury.io/gh/leviathan1995%2Ffari-proxy)

一个自由上网的代理工具, 将传输的数据加密包裹在HTTP报文, 伪装成简单的明文HTTP流量，模拟HTTP请求与响应的过程，规避其他代理因为加密特征可能被嗅探的风险, 搭配`pac`使用体验更佳.

## 特点:

* 数据包使用`aes-cfb`对称加密
* 使用HTTP协议伪装数据包, 后续会支持自定义HTTP报文
* 对本地网络软件而言, 仍然是使用的SOCKS5代理, 与浏览器等软件无缝兼容, 包括`git clone`加速
* 使用Supervisor后台运行管理
* 提供二进制可执行文件跨平台运行
* 添加`.pac`文件

## 使用方法:
请在[Release](https://github.com/Leviathan1995/fari-proxy/releases)页面下载最新版适配的二进制可执行文件
* #### 启动后台管理工具Supervisor

        supervisord -c supervisord.conf

* #### 使用Supervisor在本地机器后台启动 `client`
	
        supervisorctl start fari-client
	
* #### 在可以自由上网的服务器(VPS)使用Supervisor后台启动`server`
	
        supervisorctl start fari-server
		
* #### 在本地开启SOCKS5的代理, 例如浏览器的SOCKS5插件

### 注意:

* ##### Google Chrome 可使用SwitchyOmega或者SwitchySharp等插件配合`.pac`使用

* ##### 没有安装supervisor请自行安装
    
    ##### Debian / Ubuntu可以直接通过apt安装：
            
        # apt-get install supervisor
     
    ##### OS X 可以使用brew安装
    
        # brew install supervisor
* ##### 启动supervisord报路径错误时, 请自行`mkdir`相关路径

## 配置文件

* `.client.json`

		{
            "remote_addr" : "127.0.0.1:20010",   远程服务器监听地址
            "listen_addr" : "127.0.0.1:20011",   本地SOCKS5监听地址
            "password" : "uzon57jd0v869t7w"
		}

* `.server.json`

		{
            "listen_addr" : "127.0.0.1:20010",   远程服务器监听地址
            "password" : "uzon57jd0v869t7w"
		}

## Git clone 加速
```
git config --global http.proxy 'socks5://127.0.0.1:20010' 
git config --global https.proxy 'socks5://127.0.0.1:20010'
```

## Tips
如有任何使用问题，请在Github提交issue.

## VPS推荐
强力推荐[搬瓦工$29.9年付洛杉矶节点](https://bandwagonhost.com/aff.php?aff=35559)

## TODO

* 优化代码

* 支持多种后台运行的方法

* 支持自定义HTTP报文

* 区别国内国外IP


 
