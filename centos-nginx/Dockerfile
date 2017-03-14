FROM centos
MAINTAINER zhuyunxiang 493405455@qq.com

# 设置中国时区
ENV TZ "Asia/Shanghai"

# 线上版本需要注释掉
ENV HTTP_PROXY http://10.103.4.47:3128

# 解决公司内网使用代理上网的问题
RUN echo proxy=$HTTP_PROXY >> /etc/yum.conf

RUN	yum clean all
RUN	yum makecache

# 准备环境 安装 wget
RUN yum -y update
# 安装依赖
RUN	yum -y install gcc-c++
RUN yum -y install pcre pcre-devel  
RUN yum -y install zlib zlib-devel  
RUN yum -y install openssl openssl-devel
RUN	yum -y install wget
RUN	yum clean all

# 线上版本需要注释掉
RUN echo http_proxy=$HTTP_PROXY >> /etc/wgetrc && \
	echo ftp_proxy=$HTTP_PROXY >> /etc/wgetrc

# 下载Nginx源码包
RUN wget http://www.nginx.org/download/nginx-1.11.10.tar.gz
RUN	tar zxvf nginx-1.11.10.tar.gz && \
	rm -rf nginx-1.11.10.tar.gz

# 配置及编译Nginx
RUN cd nginx-1.11.10 && ./configure --prefix=/usr/local/nginx && make && make install

# 删除临时文件
RUN rm -rf nginx-1.11.10

# 加载本地Nginx配置
ADD ./conf/nginx.conf /usr/local/nginx/conf/nginx.conf

# 部署项目
ADD ./html /usr/local/nginx/html

# 运行Nginx
RUN /usr/local/nginx/sbin/nginx

# 暴露80端口
EXPOSE 80

# 启动Nginx
CMD ["/usr/local/nginx/sbin/nginx", "-g", "daemon off;"]
