## Uninstall old versions

```bash
$ yum remove docker \
             docker-client \
             docker-client-latest \
             docker-common \
             docker-latest \
             docker-latest-logrotate \
             docker-logrotate \
             docker-engine
```



## Set up the repository

```bash
$ yum install -y yum-utils

$ yum-config-manager \
    --add-repo \
    https://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo
    

    
# 官方源
# $ yum-config-manager \
#     --add-repo \
#     https://download.docker.com/linux/centos/docker-ce.repo

# $ sed -i 's/download.docker.com/mirrors.aliyun.com\/docker-ce/g' /etc/yum.repos.d/docker-ce.repo
```



## Install Docker Engine

```bash
$ yum install -y docker-ce docker-ce-cli containerd.io docker-compose-plugin
```



## Uninstall Docker Engine

```bash
$ yum remove docker-ce docker-ce-cli containerd.io docker-compose-plugin

$ rm -rf /var/lib/docker
$ rm -rf /var/lib/containerd
```



## Start Docker

```bash
$ systemctl start docker

$ systemctl enable docker
```



## Edit Repo

```bash
$ systemctl cat docker | grep '\-\-registry\-mirror'
# none mirror

$ vi /etc/docker/daemon.json
{
    "registry-mirrors": [
        "http://hub-mirror.c.163.com",
        "https://docker.mirrors.ustc.edu.cn",
        "https://mirror.ccs.tencentyun.com"
    ]
}

$ systemctl daemon-reload
$ systemctl restart docker

$ docker info
```

