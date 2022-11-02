```bash
$ conda info
```



```bash
$ conda config --show-sources
==> /root/.condarc <==
channels:
 - defaults
```



```bash
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free
conda config --add channels http://mirrors.aliyun.com/pypi/simple

$ conda config --add channels https://mirrors.aliyun.com/anaconda/pkgs/free
$ conda config --add channels https://mirrors.aliyun.com/anaconda/pkgs/main
$ conda config --add channels https://mirrors.aliyun.com/anaconda/pkgs/msys2
$ conda config --add channels https://mirrors.aliyun.com/anaconda/pkgs/r

$ conda config --add channels https://mirrors.aliyun.com/anaconda/cloud/

$ conda config --set show_channel_urls yes
```



```bash
conda config --remove channels 'https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free
```



```bash
$ vi /root/.condarc
ssl_verify: true
channels:
	- https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/msys2/
	- https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/conda-forge/
	- https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/
	- defaults   #---------------> 此行需要删除
show_channel_urls: true
```



```bash
# update conda
$ conda update conda

$ conda upgrade --all
```

