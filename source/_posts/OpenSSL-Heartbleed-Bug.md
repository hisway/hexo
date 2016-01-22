title: OpenSSL Heartbleed Bug
date: 2014-04-10 09:12:38
categories: 三言两语
tags: bug
---
OpenSSL被爆出严重的安全漏洞，具体请看OpenSSL官网4月7日发布的公告：<http://www.openssl.org/news/secadv_20140407.txt>
漏洞检测工具：<http://filippo.io/Heartbleed/>
该漏洞可能暴露密钥和私密通信，应尽快修补！！!

##存在此漏洞的版本情况：

1. OpenSSL 1.0.1 和OpenSSL 1.0.2-beta存在此漏洞
2. 更老版本OpenSSL(1.0.0和0.9.8)不受影响

##修补方法：

1. 如果为OpenSSL 1.0.1版本，应尽快升级到OpenSSL 1.0.1g(已修复漏洞)
2. 无法立即升级的用户可以加-DOPENSSL_NO_HEARTBEATS参数重新编译OpenSSL
3. 如果为OpenSSL 1.0.2-beta版本，建议暂时用OpenSSL 1.0.1g替代，等OpenSSL 1.0.2-beta2修复版本发布，再更新至OpenSSL 1.0.2-beta2

<!--more-->

##具体实施：

1. 检查相关服务是否有此漏洞：<http://filippo.io/Heartbleed/>
2. 查看机器上OpenSSL版本, 确认依赖OpenSSL的服务
		openssl version -a
3. 如果为OpenSSL 1.0.1[a-f] 或者 OpenSSL 1.0.2-beta版本，建议从官网下载OpenSSL 1.0.1g
		wget http://www.openssl.org/source/openssl-1.0.1g.tar.gz
		tar -zxvf openssl-1.0.1g.tar.gz && cd openssl-1.0.1g/
		./config
		make && make install
		echo "/usr/local/ssl/lib" >> /etc/ld.so.conf
		ldconfig -v
		openssl version -a 验证版本正确升级	
4. 如果不方便立即升级，建议重新下载源码加-DOPENSSL_NO_HEARTBEATS参数编译安装（OpenSSL 1.0.1e为例）
		wget http://www.openssl.org/source/openssl-1.0.1e.tar.gz
		tar -zxvf openssl-1.0.1e.tar.gz && cd openssl-1.0.1e/
		./config -DOPENSSL_NO_HEARTBEATS
		make && make install
		echo "/usr/local/ssl/lib" >> /etc/ld.so.conf
		ldconfig -v
		openssl version -a | grep DOPENSSL_NO_HEARTBEATS //验证版本正确升级
5. 确认依赖OpenSSL库的服务，例如nginx, apache等web服务，如果是静态编译了openssl库的，需要在升级完OpenSSL后重新编译服务程序，使用动态链接库的，需要重启一下服务：
		mv /usr/bin/openssl{,.OFF}
		mv /usr/include/openssl{,.OFF}
		ln -s /usr/local/ssl/bin/openssl /usr/bin/openssl
		ln -s /usr/local/ssl/include/openssl /usr/include/openssl
		echo "/usr/local/ssl/lib" >> /etc/ld.so.conf
		ldconfig -v
		openssl version -a 验证版本正确升级
6. 如果发现升级出现问题可以采用一下方法进行回滚OpenSSL
		rm -rf /usr/bin/openssl /usr/include/openssl
		mv /usr/bin/openssl{.OFF,}
		mv /usr/include/openssl{.OFF,}
		sed s#/usr/local/ssl/lib##g /etc/ld.so.conf
		ldconfig -v