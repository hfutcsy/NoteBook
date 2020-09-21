# 腾讯云服务器使用
## 登入方式
+ 腾讯云控制台扫码登入
+ SSH 登入
  ```
  ssh <username>@<hostname or IP address>
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
## 安装git

