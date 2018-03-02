# Nginx服务器简介
## 1 了解web服务器
### 1.1	什么是web服务器
> Web 服务器是指驻留于因特网上某种类型计算机的程序。当 Web 浏览器（客户端）连到服务器上并请求文件时，服务器将处理该请求并将文件发送到该浏览器上，附带的信息会告诉浏览器如何查看该文件（即文件类型）。服务器使用HTTP（超文本传输协议）进行信息交流，这就是人们常把它们称为 HTTPD 服务器的原因。
### 1.2	目前比较主流的web服务器

+ **Apache**
> Apache  仍然是世界上用得最多的 Web  服务器，市场占有率达 60%左右。它源于 NCSAhttpd  服务器，在 NCSA WWW  服务器项目停止后，那些使用 NCSA www  服务器的人们开始交换用于此服务器的补丁，这也是 Apache  名称的由来 （ pache 补丁 ) 。世界上很多著名的网站都是 Apache的用户，它的优势主要在于源代码开放、有一支开放的开发队伍、支持跨平台的应用 ( 可以运行 在几乎所有的 Unix  、Windows  、 Linux  系统平台上 )  ，以及其可移植性等。 Apache  的模块支持非常丰富，虽在速度、性能上不及其他轻量级 Web  服务器，他是属于重量级产品，所消耗的内存 也比其他 Web 服务器要高。

+	**Lighttpd**
> Lighttpd 是由一个德国人写的开源软件，其目标是提供一个专门针对高性能网站，安全、快速、兼容性好并且灵活的 Web Server 环境。它具有内存开销低、 CPU 占用率低、效能好，以及模块丰富等特点

+	**Tomcat**
> Tomcat  是一个开放源代码、运行 servlet  和 JSPWeb  应用软件的基于Java  的 Web  应用软件容 器。 Tomcat Server  是根据 servlet  和 JSP  规范执行的，因此也可以说 Tomcat Server  实行了 Apache-J akarta  规范，且比绝大多数商业应用软件服务器要好。但是， Tomcat  对静态文件、高并发的处理比较弱。

+	**IBM websphere**
> WebSphere Application Server 是一种完善、开放的 Web 应用程序服务器，是 IBM 电子商务的核心部分，它可以支持多种通用平台，因为它遵循最普及的开放标准： HTTP 、 HTML 、 JSP 、 JNDI 和 HOP 。


+	**IIS**
> iis 是 Internet Information Services 的缩写，意为互联网信息服务，是由微软公司提供的基于运行 Microsoft Windows 的互联网基本服务。IS 是一种 Web （网页）服务组件，其中包括 Web 服务器、 FTP 服务器、 NNTP 服务器和 SMTP 服务器，分别用于网页浏览、文件传输、新闻服务和邮件发送等方面，它使得在网络（包括互联网和局域网）上发布信息成了一件很容易的事。

### 1.3	当前主流web服务器市场情况
根据2016年11月的web服务器调查（在2016次调查中，收到了来自1436724046个网站和6225374个面向Web的计算机的响应）
![image](C:/Users/Administrator/Desktop/培训：nginx/服务器用户图.png)
### 1.4	对比较常见的几个服务器进行比较
![image](C:/Users/Administrator/Desktop/培训：nginx/服务器性能比较.png)
通过比较我们可以看出，nginx在反向代理商，rewrite规则，稳定性，静态文件处理
上，内存消耗等方面都表现出很强的优势。
那我们就详细的了解下ngix的相关内容

## 2	关于nginx
### 2.1	nginx的简史
nginx是俄罗斯人igor sysoev在2004年编写的一款高性能的http和反向代理服务器。
nginx选择了epoll和kqueue作为网络i/o模型，在高连接并发的情况下，内存、cpu等系
统资源消耗非常低，运行稳定。其实apache服务器最好的替代品，它能够支持高达
50000个并发连接数。

### 2.2	nginx的相关产品
2.2.1	nginx最初为一款软件，后来成立了nginx公司（NGINX Inc），目前其旗下主要产品两个
- 开源产品 nginx
- 收费产品 nginx plus ### 2.3，为什么选择nginx Nginx 是一个高性能的 Web 和反向
代理服务器， 它具有有很多非常优越的特性:

**作为 Web 服务器：** 相比 Apache，Nginx 使用更少的资源，支持更多的并发连接，体现
更高的效率，这点使 Nginx 尤其受到虚拟主机提供商的欢迎。能够支持高达 50，000
个并发连接数的响应，感谢 Nginx 为我们选择了 epoll and kqueue 作为开发模型.

**作为负载均衡服务器：** Nginx 既可以在内部直接支持 Rails 和 PHP，也可以支持作为
HTTP代理服务器 对外进行服务。Nginx 用 C 编写， 不论是系统资源开销还是 CPU 使
用效率都比 Perlbal 要好的多。
**作为邮件代理服务器: ** Nginx 同时也是一个非常优秀的邮件代理服务器（最早开发这个
产品的目的之一也是作为邮件代理服务器），Last.fm 描述了成功并且美妙的使用经验。

**其他：** Nginx 安装非常的简单，配置文件 非常简洁（还能够支持perl语法），Bugs非
常少的服务器: Nginx 启动特别容易，并且几乎可以做到7*24不间断运行，即使运行数
个月也不需要重新启动。你还能够在 不间断服务的情况下进行软件版本的升级。
## 2.3	nginx的优势
- nginx可以高并发连接

> 官方测试 Nginx 能够支撑 5 万并发连接，实际测试可以达到 3 万左右，按照这样计算，每天可以处理亿次访问量，采用最新epoll （ Linux 2.6 内核）和 kqueue （ freebsd ）网络 I/O 模型，而 Apache则使用的是传统的 select 模型。
- nginx 内存消耗更少
> Nginx+PHP （ FastCGI ）服务器在 3 万并发连接下，开启 10 个 Nginx 进
> 程消耗 150MB 内存（ 15MBX10 ），开启 64 个 php-cgi 进程消耗 128MB
> 内存（ 20MB x 64 ），使用 Webbench 做压力测试，在 3 万并发量下速
> 度依然很快。
- 成本低廉
> 在负载均衡方面，其不需要购买硬件设备即可完成。 nginx 采用 2-
> clause-BSD-like 协议，可以免费试用，并可以用于商业用途。
- 配置文件简单
> 配置文件超简单，即使非管理人员也能看懂。
- 支持rewrite规则
> 根据域名， URL 的不同，可以请求分发到不同主机上。
- 内置健康检查
> 通过反向代理到后台的主机，即使主机宕机也不会影响到服务器的访问。
- 节省带宽

> 支持 Gzip 压缩，可以在浏览器本地缓存的 header 中。
- 稳定性高
- 支持热部署

## 3	nginx的安装与简单配置
### 3.1	nginx主要功能
#### 3.1.1	HTTP基础功能：
- 处理静态文件，索引文件以及自动索引；
- 反向代理加速(无缓存)，简单的负载均衡和容错；
- FastCGI，简单的负载均衡和容错；
- 模块化的结构。过滤器包括gzipping， byte ranges， chunked responses， 以及SSI-filter 。在SSI过滤器中，到同一个 proxy 或者 FastCGI 的多个子请求并发处理；
- SSL 和 TLS SNI 支持。
#### 3.1.2	IMAP/POP3 代理服务功能：
- 使用外部 HTTP 认证服务器重定向用户到 IMAP/POP3 后端；
- 使用外部 HTTP 认证服务器认证用户后连接重定向到内部的 SMTP 后端；
- 认证方法：
  - POP3: POP3 USER/PASS， APOP， AUTH LOGIN PLAIN CRAM-MD5;
  - IMAP: IMAP LOGIN;
  - SMTP: AUTH LOGIN PLAIN CRAM-MD5;
- SSL 支持；
  - 在 IMAP 和 POP3 模式下的 STARTTLS 和 STLS 支持；
#### 3.1.3	结构与扩展：
- 一个主进程和多个工作进程。工作进程是单线程的，且不需要特殊授权即可运行；
- kqueue (FreeBSD 4.1+)， epoll (Linux 2.6+)， rt signals (Linux 2.2.19+)， /dev/poll
- (Solaris 7 11/99+)， select， 以及 poll 支持；
- kqueue支持的不同功能包括 EV_CLEAR， EV_DISABLE （临时禁止事件），
- NOTE_LOWAT， EV_EOF， 有效数据的数目，错误代码；
- sendfile (FreeBSD 3.1+)， sendfile (Linux 2.2+)， sendfile64 (Linux 2.4.21+)， 和
- sendfilev (Solaris 8 7/01+) 支持；
- 输入过滤 (FreeBSD 4.1+) 以及 TCP_DEFER_ACCEPT (Linux 2.4+) 支持；
- 10，000 非活动的 HTTP keep-alive 连接仅需要 2.5M 内存。
- 最小化的数据拷贝操作；
#### 3.1.4 其他HTTP功能：
- 基于IP 和名称的虚拟主机服务；
- Memcached 的 GET 接口；
- 支持 keep-alive 和管道连接；
- 灵活简单的配置；
- 重新配置和在线升级而无须中断客户的工作进程；
- 可定制的访问日志，日志写入缓存，以及快捷的日志回卷；
- 4xx-5xx 错误代码重定向；
- 基于 PCRE 的 rewrite 重写模块；
- 基于客户端 IP 地址和 HTTP 基本认证的访问控制；
- PUT， DELETE， 和 MKCOL 方法；
- 支持 FLV （Flash 视频）；
- 带宽限制；

### 3.2	nginx的安装
nginx的根据不同的系统有不同的安装方案
- window
  - 使用nginx的exe安装包一键安装
- linux
  - 源码安装（参见nginx 源码安装流程）
  - 根据系统版本安装（apt yum）
- mac os
  - 在mac下通过brew安装nginx

### 3.3	nginx的常用操作
#### 3.3.1	方法1)通过信号量来操作
nginx中可以通过linux中的信号量的方式来对nginx进行操作

**信号量：** 信号量的使用主要是用来保护共享资源，使得资源在一个时刻只有一个进程
（线程）所拥有。信号量的值为正的时候，说明它空闲。所测试的线程可以锁定而使
用它。若为0，说明它被占用，测试的线程要进入睡眠队列中，等待被唤醒。

```
用法：kill -信号量量选项 nginx的主进程号
```
nginx的信号量选项：

信号量选项 | 描述
------|-----------
TERM |快速的关闭nginx的进程
INT |快速的关闭nginx的进程
QUIT |请求结束后关闭nginx进程
HUP |平滑的重新读取配置文件
USR1 |平滑的读写日志文件
USR2 |平滑的升级
WINCH |优雅的关闭nginx进程(等nginx空闲时关闭)
如：

```
kill -TREM 4129
```
#### 3.3.2，方案2)通过nginx的二进制文件来操作
nginx的二进制文件在安装目录下的sbin下:、/usr/local/nginx/sbin/nginx
> 基本用法：/usr/local/nginx/sbin/nginx -s 操作

操作| 命令
---|---
启动nginx:| /usr/local/nginx/sbin/nginx
关闭nginx:| /usr/local/nginx/sbin/nginx -s stop
退出nginx:| /usr/local/nginx/sbin/nginx -s quit
重新读取配置文件:| /usr/local/nginx/sbin/nginx -s reload
重启: |/usr/local/nginx/sbin/nginx -s reopen

其他用法：

```
nginx -v 查看当前nginx版本
nginx -h 查看nginx⽤用法
nginx -t 测试当前配置⽂文件是否正确
```
## 四，nginx的深入
### 4.1，nginx的基本配置
在安装完成nginx后，活在系统的/etc/下产生一个nginx目录，该目录用于存放nginx的
常用配置文件，正常情况下nginx已经给定了默认的配置文件，但我们现在需要根据需
求晚上相应的nginx配置。
#### 4.1.1，nginx的基本配置
此处配置一个最基本的实例

**vim /etc/nginx/nginx.conf**

```
# 使用的用户组
user nginx;
# 指定工作衍生进程数 此处设置为auto，根据需求生成
worker_processes auto;
# 指定错误日志存在位置
error_log /var/log/nginx/error.log;
# 指定nginx的pid存放路路径
pid /var/run/nginx.pid;
# Load dynamic modules. See /usr/share/nginx/README.dynamic.
include /usr/share/nginx/modules/*.conf;
events {
# 此处可指定使用的I/O模型
# use epoll（默认使用）
# 允许的连接数个数，即每个worker进程能并发处理理的最大连接数
worker_connections 1024;
}
http {
# 设置一个名字为maim的log日志格式
log_format main '$remote_addr - $remote_user [$time_local] "$requ
est" '
'$status $body_bytes_sent "$http_referer" '
'"$http_user_agent" "$http_x_forwarded_for"';
# access_log /var/log/nginx/access.log main;
sendfile on;
tcp_nopush on;
tcp_nodelay on;
keepalive_timeout 65;
types_hash_max_size 2048;
# 设置使用的字符集
include /etc/nginx/mime.types;
default_type application/octet-stream;
server
{
lisen 80；
server_name www.xxx.com;
index.html index.htm index.php;
root /var/www/html
location / {
}
# 当返回码为404时指向404.html页面
error_page 404 /404.html;
location = /40x.html {
}
# 当500 502 503 504
error_page 500 502 503 504 /50x.html;
location = /50x.html {
}
}
# Load modular configuration files from the /etc/nginx/conf.d direc
tory.
# See http://nginx.org/en/docs/ngx_core_module.html#include
# for more information.
include /etc/nginx/conf.d/*.conf;
}
```
从上述的文件可以看出，nginx.conf 文件的主要结构为

```
......
events{
    ......
}
......
http{
    ......
    server
    {
    ......
    }
    ......
    server
    {
    ......
    }
......
}
```
#### 4.1.2，nginx的虚拟主机配置
**什么是虚拟主机?**

++虚拟主机使用的是特殊的软硬件技术，把一台运行行在英特网上的服务器器主机分成一台台“虚拟”的主机，
每台虚拟主机都可以是一个独立的网站。可以具有独立的域名。具有完整的Internet服务器器的功能。
同一台主机上的虚拟主机之间是完全独立的。从网站的访问者来看，每台虚拟主机和一台独立的主机完
全相同。简单的说，虚拟主机就是提供了了在同一台服务器器上，同一组nginx进程上运行多个网站的功
能。++
**如下为一个最简单的虚拟主机配置**


```
http {
server
{
lisen 80；#虚拟主机的不不同端口
server_name www.xxx.com *.xxx.com; #此处可以填写ip 或者域名 多个域名
access_log /var/log/acceess1.log combined;
location / {
index index.html index.php;
root /var/www/html1
}
}
server
{
lisen 8080；#虚拟主机的不不同端⼝口
server_name www.xxx2.com; #此处可以填写ip 或者域名
access_log /var/log/acceess2.log combined;
location / {
index index.html index.php;
root /var/www/html2
}
}
server
{
lisen 8888；#虚拟主机的不不同端⼝口
server_name 10.60.0.12; #此处可以填写ip 或者域名
access_log /var/log/acceess3.log combined;
location / {
index index.html index.php;
root /var/www/html3
}
}
}
```
nginx 虚拟主机和apache的vhost一样，可以设置
> 1. 基于IP的虚拟主机和
> 1. 基于域名的虚拟主机或者
> 1. 基于端口的虚拟主机

这三种不同的虚拟主机的主要配置不同为监听的端口不同，或者使用的server_name不
同。

### 4.2，nginx的优化
#### 4.2.1，nginx的日志优化


log_format 用来设置日志的记录。用户可以根据自己的需求修改日志的格式，其语法如下
```
log_formate name（命名不不能重复） format [....]
```
access_log 用来指定日志文件的存放路径，access_log指令的用法如下


```
access_log path [form [buffer=size|off] ]
```
- path:指的是存放路径
- format：使用log_format指令设置的日志格式名称。
- buffer:表示内存缓冲区的大小

关闭access日志

```
access_log off;
```
设置日志的格式为combined

```
access_log /xxx/xxxx.log;
或者
access_log /xxx/xxxx.log combined;
```
可在access中设置变量，其好处是可以对日志进行分割，比如按照每天或没小时进行分割

eg:

```
if ($time_iso8601 ~ "^(\d{4})-(\d{2})-(\d{2})T(\d{2}):(\d{2}):(\d{2})")
{
set $year $1;
set $month $2;
set $day $3;
set $hour $4;
set $minutes $5;
set $seconds $6;
}
location /cmps/admin.php/api/ping {
。。。。。。
}
# 即可按照每天进⾏行行⽇日志分割
access_log /var/log/nginx/$year-$month-$day-cmps-access-ping.log main
;
```
#### 4.2.2 nginx的压缩输出配置

着网站内容不断增加，我们的网站上的内容和功能也变得丰富多彩，这时就会有一个
问题出现----我们的网站加载会明显变慢，这对于网站的访客来说可不是一件愉快的
事，那么我们该如何优化网站，加快网站的访问速度呢？减少网站的文件内容是不可
能了，但我们可以用一种“魔法”把这些文件变小，下面我们便来认识一下这个奇妙的缩
小术-----gzip。

gzip(GNU-ZIP)是一种压缩技术，经过它的压缩，页面大小会缩小到一种可观的比例，
它的原理就是在服务器端进行压缩，当压缩后的数据包到达用户端的浏览器时，会进
行解压，还原出原来的内容，压缩过程，用户在访问网站时并不会感觉到。所以gzip
的压缩需要浏览器和服务器双方面的支持。不过不需要我们担心，因为IE、火狐、
Opera、谷歌等绝大多数浏览器都支持解析gzip过的页面。

Nginx的压缩输出由一组gzip压缩指令来实现。gzip压缩输出的相关指令位于http{......}
两个大括号之间：


```
# 指令⽤用于开启或关闭gzip模块。默认为off
gzip on;
# 设置允许压缩的⻚页⾯面最⼩小字节数，⻚页⾯面字节数从header头的Content-Length中进⾏行行获取。
默认值是0，不不管⻚页⾯面多⼤大都压缩。建议设置成⼤大于1k的字节数，⼩小于1k的可能越压越⼤大。即：gz
ip_min_length 1024。
gzip_min_length 1k;
# 设置系统获取⼏几个单位的缓存⽤用户存储gzip的压缩结果数据流。例例如4 4k代表以4k为单位，按
照原始数据⼤大⼩小以4k为单位的4倍申请内存。4 8k代表以8k为单位，按照原始数据以8k为单位的4
倍申请内存。
# 如果没有设置，默认值是申请跟原始数据相同⼤大⼩小的内存空间去存储gzip压缩结果
gzip_buffers 4 16k;
# 识别http的协议版本。由于早期的⼀一些浏览器器或http客户端，肯能不不⽀支持gzip⾃自解压，⽤用户
会看到乱码，所以做⼀一些判断还是有必要的。
gzip_http_version 1.1;
#gzip压缩⽐比，1：压缩⽐比最⼩小，处理理速度最快，9：压缩⽐比最⼤大但处理理速度最慢（传输快但更更消耗
CPU）。⼀一般设置为3即可。
gzip_comp_level 2;
# 匹配mime类型进⾏行行压缩，（⽆无论是否指定）“text/html”类型总是会被压缩的
gzip_types text/plain application/x-javascript text/css application/xml
;
```

#### 4.2.3，nginx的自动列目录配置
Nginx默认是不允许列出整个目录的。如需此功能，打开nginx.conf文件或你要启用目
录浏览虚拟主机的配置文件，在server或location 段里添加上 **autoindex on**;

另外Nginx的目录流量有两个比较有用的参数，可以根据自己的需求添加：


```
autoindex_exact_size off;
## 默认为on，显示出⽂文件的确切⼤大⼩小，单位是bytes。
## 改为off后，显示出⽂文件的⼤大概⼤大⼩小，单位是kB或者MB或者GB
autoindex_localtime on;
## 默认为off，显示的⽂文件时间为GMT时间。
## 改为on后，显示的⽂文件时间为⽂文件的服务器器时间
```
#### 4.2.4，nginx的浏览器本地缓存设置
浏览器缓存是为了加速浏览，浏览器在用户磁盘上对最近请求过的文档进行存储，当
访问者再次请求这个页面时，浏览器就可以从本地磁盘显示 文档，这样就可以加速页
面的浏览。缓存 的方式节约了网络的资源，提高网络的效率。

nginx可以通过 expires 指令来设置浏览器的Header

- 语法： expires [time|epoch|max|off]
- 默认值： expires off
- 作用域： http， server， location
eg:

```
# 图⽚片缓存
location ~.*\.(jpg|png|jpeg)$
{
expires 30d;
}
# js css缓存⼀一⼩小时
location ~.*\.(js|css)?$
{
expires 1h;
}
```
这儿几个常见的优化就完成。

