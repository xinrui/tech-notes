# 怎么在虚拟机中，使用宿主机的代理翻墙？

## 概况
宿主机：windows 11  
虚拟机：hyper V + ubuntu 24.04 LTS  
翻墙工具：v2rayN v7.14.6

## 方法
1. 打开v2rayN -> 设置 -> 参数设置 -> Core：基础设置 -> **允许来自局域网的连接**
2. 在宿主机使用`ipconfig`命令，找到网关的IPv4地址（我的地址：172.21.112.1）
3. 在虚拟机上`ping`一下网关，确保能`ping`通
4. 在系统设置里，看一下代理服务器的端口（我的端口：10808）
5. 如果想在终端中联网，设置环境变量`http_proxy`和`https_proxy`
```bash
export http_proxy=socks5://172.21.112.1:10808
export https_proxy=socks5://172.21.112.1:10808
```
想在浏览器中联网，就设置浏览器代理。  
如果宿主机ip固定，可以不用网关

## 补救
宿主机重启之后网关可能发生变化，为了避免设置失效，新版的Hyper V支持这种设置：
```bash
export http_proxy=http://host.docker.internal:10808
export https_proxy=http://host.docker.internal:10808
```

## 命令拾遗
`ip route | grep default` 解析出默认网关
`nc -vz 172.21.112.1 10808` 测试端口