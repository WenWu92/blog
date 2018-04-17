#### 下载haproxy最新包
    wget http://www.haproxy.org/download/1.6/src/haproxy-1.6.14.tar.gz
#### 解压
    tar zxvf haproxy-1.6.14.tar.gz
#### 安装
    make TARGET=linux2628 PREFIX=/usr/local/haproxy
    make install PREFIX=/usr/local/haproxy
#### 修改配置文件
    /usr/local/haproxy/haproxy.cfg
#### 配置文件模板
    global
        ulimit-n  51200
    defaults
        log global
        mode    tcp
        option  dontlognull
        timeout connect 1000
        timeout client  150000
        timeout server 150000
    frontend ss-in
        bind *:8388
        default_backend transfer-out
    backend transfer-out
        server server1 目标IP:端口 maxconn 20480
#### 启动服务
    /usr/local/haproxy/sbin/haproxy -f /usr/local/haproxy/haproxy.cfg
#### 开机自启
    vi /etc/rc.local
#### 添加
    /usr/local/haproxy/sbin/haproxy -f /usr/local/haproxy/haproxy.cfg
