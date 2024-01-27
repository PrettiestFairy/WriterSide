# RHEL9系统初始化

## 添加 yum 源

### EPEL(epel-release)

```Shell
subscription-manager repos --enable codeready-builder-for-rhel-9-$(arch)-rpms
dnf install https://dl.fedoraproject.org/pub/epel/epel-release-latest-9.noarch.rpm
```

## 关闭 selinux

```Shell
# 临时禁用
setenforce 0
# 永久禁用(需重启)
sudo sed -i 's/^SELINUX=enforcing/SELINUX=disabled/' /etc/selinux/config
sudo sed -i 's/^SELINUX=permissive/SELINUX=disabled/' /etc/selinux/config
```

## 安装 Docker

卸载 Podman 和相关工具

```Shell
sudo dnf remove podman buildah
```
   
安装 Docker CE

```Shell
sudo dnf config-manager --add-repo=https://download.docker.com/linux/centos/docker-ce.repo
sudo yum install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
# 如果有依赖冲突
sudo yum install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin --nobest
```

