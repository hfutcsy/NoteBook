# 腾讯云服务器使用
## 登入方式
+ 腾讯云控制台扫码登入
+ SSH 登入
  ```
  ssh <username>@<hostname or IP address> -p portalnumber
  ```
## 查看linux系统CPU及version
  ```
  # 查看CPU信息
  cat /proc/cpuinfo
  
  # 查看CentOS版本
  cat /etc/redhat-release 
  ```
## 修改为阿里yum源-mirrors.aliyun.com
1、首先备份系统自带yum源配置文件/etc/yum.repos.d/CentOS-Base.repo

`[root@localhost ~]# mv /etc/yum.repos.d/CentOS-Base.repo /etc/yum.repos.d/CentOS-Base.repo.backup`

2、查看CentOS系统版本

`[root@localhost ~]# lsb_release -a`

3、下载ailiyun的yum源配置文件到/etc/yum.repos.d/
 ```
 # CentOS7
 [root@localhost ~]# wget -O /etc/yum.repos.d/CentOS-Base.repo http://mirrors.aliyun.com/repo/Centos-7.repo
 ```

4、运行yum makecache生成缓存

`[root@localhost ~]# yum makecache`

## 安装node环境
```
# As root
curl -sL https://rpm.nodesource.com/setup_lts.x | bash -

# No root privileges 
curl -sL https://rpm.nodesource.com/setup_lts.x | sudo bash -

sudo yum install -y nodejs
```
## 安装git
安装官网<https://git-scm.com/download/linux>
测试环境为Centos7，官网提到centos7默认的yum只有很旧的低版本git。所以推荐下载源码编译安装。
### 卸载老版本
```
# 查看版本
git --version

# 卸载老版本
yum remove git
```
### 安装依赖包
`yum install curl-devel expat-devel gettext-devel openssl-devel zlib-devel gcc perl-ExtUtils-MakeMaker`
### 下载源代码
下载地址<https://mirrors.edge.kernel.org/pub/software/scm/git/>
挑选最新的版本拷贝链接，以2.9.5 为例。

`wget https://mirrors.edge.kernel.org/pub/software/scm/git/git-2.9.5.tar.gz`
### 解压安装
```
tar -zxvf git-2.9.5.tar.gz
cd git-2.9.5
./configure --prefix=/usr/local/git
make && make install
```

### 添加环境变量

`vim /etc/profile`

文件最后一行添加

`export PATH=$PATH:/usr/local/git/bin`

刷新环境变量：
```
source /etc/profile
```
### 查看版本
`git version`

## Https配置
[在腾讯云上搭建SSL证书实现https访问（Nginx)](https://segmentfault.com/a/1190000015583348)

## 解决Github clone速度慢的问题
github 的库在国内比较慢，我们可以将github 的库导入到gitee上，然后通过从gitee 上clone，再修改远程库源地址
```
# 查看源地址
git remote -v

#修改源地址
git remote set-url origin [new url]
```
## 安装配置Nginx
### Nginx安装
[参考链接]<https://www.cnblogs.com/xxoome/p/5866475.html>
+ Nginx 安装地址 <https://nginx.org/download>
选择最新稳定版本nginx-1.18.0.tar.gz下载
```
# 下载
wget https://nginx.org/download/nginx-1.18.0.tar.gz

# 解压
tar -zxvf nginx-1.18.0.tar.gz

# 进入nginx目录
cd nginx-1.9.9

# 配置
./configure --prefix=/usr/local/nginx

# make
make
make install

# 测试是否安装成功
cd /usr/loca/nginx/
./sbin/nginx -t

# 启动nginx
cd /usr/local/nginx/sbin
./nginx //启动nginx
```
### Nginx配置
+ 配置自启动
```
vim /etc/rc.d/rc.local

# touch那一行下添加一行
/usr/local/nginx/sbin/nginx

```

## 安装mysql
[参考链接]<https://www.runoob.com/mysql/mysql-install.html>
yum默认的下载列表里没有mysql，所以先下载资源包。
资源包地址
<https://dev.mysql.com/downloads/>

```
# 下载资源包
wge https://dev.mysql.com/get/mysql80-community-release-el7-3.noarch.rpm

rpm -ivh mysql-community-release-el7-5.noarch.rpm
yum update
yum install mysql-server
```
+ mysql 日志中可以查看初始密码

`vim /var/log/mysqld.log`
+ 改变初始密码
`mysqladmin -u root -p password [newpassword]`
然后输入旧密码
