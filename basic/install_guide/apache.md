# 安装和部署

## Apache

Apache是流行的Web服务器，官网为[http://httpd.apache.org/](http://httpd.apache.org/)。

PHP应用的部署很多都是选择Nginx+php-fpm或者Apache+mod_php的模式，单纯比较Nginx和Apache在高并发方面的性能，Nginx的表现更优。但是就PHP的CGI而言，并没有很大的差距。可以根据实际的技术积累和使用经验来进行选择。

refork、Worker、Event三者粗略介绍：

（1）prefork，多进程模式，1个进程服务于1个用户请求，成本比较高。但是，稳定性最高，不需要支持线程安全。
（2）worker，多进程多线程模式，1个进程含有多个worker线程，1个worker线程服务于1个用户请求，因为线程更轻量，成本比较低。但是，在KeepAlive场景下，worker资源会被client占据，无法响应其他请求（空等待）。
（3）event，多进程多线程模式，1个进程也含有多个worker线程，1个worker线程服务于1个用户请求。但是，它解决了KeepAlive场景下的worker线程被占据问题，它通过专门的线程来管理这些KeepAlive连接，然后再分配“工作”给具体处理的worker，工作worker不会因为KeepAlive而导致空等待。