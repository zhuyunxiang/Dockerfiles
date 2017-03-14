FROM centos
MAINTAINER zhuyunxiang 493405455@qq.com

# 设置中国时区
ENV TZ "Asia/Shanghai"

# 线上版本需要注释掉
# ENV HTTP_PROXY http://10.103.4.47:3128

# 解决公司内网使用代理上网的问题
# RUN echo proxy=$HTTP_PROXY >> /etc/yum.conf

RUN	yum clean all
RUN	yum makecache

# 准备环境 安装 wget
RUN yum -y update
# 安装依赖
RUN	yum -y install gcc
RUN	yum -y install gcc-c++
RUN yum -y install pcre pcre-devel  
RUN yum -y install zlib zlib-devel  
RUN yum -y install openssl openssl-devel
RUN	yum -y install wget
RUN	yum clean all

# 线上版本需要注释掉
# RUN echo http_proxy=$HTTP_PROXY >> /etc/wgetrc && \
#	echo ftp_proxy=$HTTP_PROXY >> /etc/wgetrc

# 下载Node源码包
RUN wget http://nodejs.org/dist/v6.10.0/node-v6.10.0.tar.gz
RUN	tar zxvf node-v6.10.0.tar.gz && \
	rm -rf node-v6.10.0.tar.gz

# 配置及编译Node
RUN cd node-v6.10.0 && ./configure --prefix=/usr/local/node && make && make install

# 删除临时文件
RUN rm -rf node-v6.10.0

# 配置环境变量 
ENV NODE_HOME /usr/local/node
ENV PATH $NODE_HOME/bin:$PATH
ENV NODE_PATH $NODE_HOME/lib/node_modules:$PATH

# 暴露80端口
# EXPOSE 80

# 启动
CMD ["/bin/bash", "-g", "daemon off;"]
