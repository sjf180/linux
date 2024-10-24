# arm(arrch64)架构下基于centos7打包生成openssh升级的rpm文件


参考内容：[openssh-rpms](https://github.com/boypt/openssh-rpms)

支持以下系统：

- CentOS 5/6/7/8/Stream 8/9
- Amazon Linux 1/2/2023
- UnionTech OS Server 20
- openEuler 22.03 (LTS-SP1)
- AnolisOS 7.9/8.6



## 1. 下载编译用的文件

1. 克隆[openssh-rpms](https://github.com/boypt/openssh-rpms.git)仓库代码
2. 下载[openssl-1.1.1w](https://github.com/openssl/openssl/releases/download/OpenSSL_1_1_1w/openssl-1.1.1w.tar.gz)
3. 下载[openssh-9.9p1](https://mirrors.aliyun.com/pub/OpenBSD/OpenSSH/portable/openssh-9.9p1.tar.gz)



## 2. 编译制作rpm包

1. 将下载好的压缩包存放至openssh-rpms/downloads目录
2. 将version.env内的OPENSSLSRC=openssl-3.0.15.tar.gz修改为OPENSSLSRC=openssl-1.1.1w.tar.gz

``` sh
cd openssh-rpms
./pullsrc.sh
```

3. 安装编译依赖

```sh
yum groupinstall -y "Development Tools"
yum install -y imake rpm-build pam-devel krb5-devel zlib-devel libXt-devel libX11-devel gtk2-devel perl perl-IPC-Cmd

# For CentOS5 only:
yum install -y gcc44
```

4. 如编译适用于centos7的rpm包

```sh
./compile.sh el7
```

5. 查看编译内容

```sh
ls -lh el7/RPMS/aarch64/

-rw-r--r-- 1 root root 4.5M 9月  25 13:50 openssh-9.9p1-1.el7.aarch64.rpm
-rw-r--r-- 1 root root 4.6M 9月  25 13:50 openssh-clients-9.9p1-1.el7.aarch64.rpm
-rw-r--r-- 1 root root 4.6M 9月  25 13:50 openssh-debuginfo-9.9p1-1.el7.aarch64.rpm
-rw-r--r-- 1 root root 2.5M 9月  25 13:50 openssh-server-9.9p1-1.el7.aarch64.rpm
 
ls -lh el7/SRPMS/

-rw-r--r-- 1 root root 12M 9月  25 13:50 openssh-9.9p1-1.el7.src.rpm
```

6. 安装依赖

```sh
yum localinstall *.rpm
```

## 3. centos7 arm架构的下载链接

[点击下载](./centos7-aarch64.zip)

