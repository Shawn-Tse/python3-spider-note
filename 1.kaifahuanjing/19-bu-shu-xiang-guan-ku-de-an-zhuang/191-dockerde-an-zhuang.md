## Docker 是什么 {#Docker入门-Docker是什么}

Docker 是一种容器技术，它可以将应用和环境等进行打包，形成一个独立的，类似于 iOS 的 APP 形式的「应用」，这个应用可以直接被分发到任意一个支持 Docker 的环境中，通过简单的命令即可启动运行。Docker 是一种最流行的容器化实现方案。和虚拟化技术类似，它极大的方便了应用服务的部署；又与虚拟化技术不同，它以一种更轻量的方式实现了应用服务的打包。使用 Docker 可以让每个应用彼此相互隔离，在同一台机器上同时运行多个应用，不过他们彼此之间共享同一个操作系统。Docker 的优势在于，它可以在更细的粒度上进行资源的管理，也比虚拟化技术更加节约资源。

[官方文档](http://guide.daocloud.io/dcs/docker-9152673.html)

### 1. 相关链接 {#1-相关链接}

* 官方网站：[https://www.docker.com](https://www.docker.com/)
* GitHub：[https://github.com/docker](https://github.com/docker)
* Docker Hub：[https://hub.docker.com](https://hub.docker.com/)
* 官方文档：[https://docs.docker.com](https://docs.docker.com/)
* DaoCloud：[http://www.daocloud.io](http://www.daocloud.io/)
* 中文社区：[http://www.docker.org.cn](http://www.docker.org.cn/)
* 中文教程：[http://www.runoob.com/docker/docker-tutorial.html](http://www.runoob.com/docker/docker-tutorial.html)
* 推荐书籍：[https://yeasy.gitbooks.io/docker\_practice](https://yeasy.gitbooks.io/docker_practice)

### 2.在windows下安装

Windows10 64位安装:推荐使用 [Docker for Windows](https://docs.docker.com/docker-for-windows/install/)

非Windows10 64位系统安装:[https://docs.docker.com/toolbox/toolbox\_install\_windows/](https://docs.docker.com/toolbox/toolbox_install_windows/)

这里以VMware Workstation为例:

#### 环境:

* Hyper-V：已卸载
* VMware：已安装
* Virtual Box：无安装

#### 驱动

下载地址:[https://github.com/pecigonzalo/docker-machine-vmwareworkstation/releases/latest](https://github.com/pecigonzalo/docker-machine-vmwareworkstation/releases/latest)

#### 复制

* 通过InstallDocker.msi安装的，复制到C:\Program Files\Docker\Docker\resources\bin下

* 通过DockerToolbox.exe安装的，复制到C:\Program Files\Docker Toolbox下

#### 打开**git-bash**，输入以下命令：

`docker-machine ls`

![](/assets/1.9.1-3.png)

检查是否有machine实例，如果有，请考虑是否卸载它

```
docker-machine stop dev && docker-machine rm dev
```

停止NAME为name的machine实例

```
docker-machine stop name
```

删除NAME为name的machine实例

```
docker-machine rm name
```

创建一个名称为dev的machine实例

```
docker-machine create --driver=vmwareworkstation dev
```

## 使用Docker Toolbox进行安装

1. 不使用VirtualBox安装Docker Toolbox

   `DockerToolbox-.exe /COMPONENTS="Docker,DockerMachine"`

2. `C:\Program Files\Docker Toolbox\start.sh`用此脚本替换内容。

```
!/bin/bash
export PATH="$PATH:/mnt/c/Program Files (x86)/VMware/VMware Workstation"
trap '[ "$?" -eq 0 ] || read -p "Looks like something went wrong in step ´$STEP´... Press any key to continue..."' EXIT
VM=${DOCKER_MACHINE_NAME-default}
DOCKER_MACHINE=./docker-machine.exe
BLUE='\033[1;34m'
GREEN='\033[0;32m'
NC='\033[0m'
if [ ! -f "${DOCKER_MACHINE}" ]; then
     echo "Docker Machine is not installed. Please re-run the Toolbox Installer and try again."
     exit 1
   fi
vmrun.exe list | grep \""${VM}"\" &> /dev/null
   VM_EXISTS_CODE=$?
set -e
STEP="Checking if machine $VM exists"
   if [ $VM_EXISTS_CODE -eq 1 ]; then
     "${DOCKER_MACHINE}" rm -f "${VM}" &> /dev/null || :
     rm -rf ~/.docker/machine/machines/"${VM}"
 #set proxy variables if they exists
 if [ -n ${HTTP_PROXY+x} ]; then
   PROXY_ENV="$PROXY_ENV --engine-env HTTP_PROXY=$HTTP_PROXY"
 fi
 if [ -n ${HTTPS_PROXY+x} ]; then
   PROXY_ENV="$PROXY_ENV --engine-env HTTPS_PROXY=$HTTPS_PROXY"
 fi
 if [ -n ${NO_PROXY+x} ]; then
   PROXY_ENV="$PROXY_ENV --engine-env NO_PROXY=$NO_PROXY"
 fi  
 "${DOCKER_MACHINE}" create -d vmwareworkstation $PROXY_ENV "${VM}"
fi
STEP="Checking status on $VM"
   VM_STATUS="$(${DOCKER_MACHINE} status ${VM} 2>&1)"
   if [ "${VM_STATUS}" != "Running" ]; then
     "${DOCKER_MACHINE}" start "${VM}"
     yes | "${DOCKER_MACHINE}" regenerate-certs "${VM}"
   fi
STEP="Setting env"
   eval "$(${DOCKER_MACHINE} env --shell=bash ${VM})"
STEP="Finalize"
   clear
   cat << EOF
                       ##         .
                 ## ## ##        ==
              ## ## ## ## ##    ===
          /"""""""""""""""""\___/ ===
     ~~~ {~~ ~~~~ ~~~ ~~~~ ~~~ ~ /  ===- ~~~
          \______ o           __/
            \    \         __/
             \____\_______/
EOF
   echo -e "${BLUE}docker${NC} is configured to use the ${GREEN}${VM}${NC} machine with IP ${GREEN}$(${DOCKER_MACHINE} ip ${VM})${NC}"
   echo "For help getting started, check out the docs at 
https://docs.docker.com
"
   echo
   cd
docker () {
     MSYS_NO_PATHCONV=1 docker.exe "$@"
   }
   export -f docker
if [ $# -eq 0 ]; then
     echo "Start interactive shell"
     exec "$BASH" --login -i
   else
     echo "Start shell with command"
     exec "$BASH" -c "$*"
   fi
```

然后与上面同样的操作

### 验证安装

```
docker run hello-world
```

### 镜像加速

安装好 Docker 之后，在运行测试命令时，我们会发现它首先会下载一个 Hello World 的镜像，然后将其运行，但是下载速度有时候会非常慢，这是因为它默认还是从国外的 Docker Hub 下载的，所以为了提高镜像的下载速度，我们还可以使用国内镜像来加速下载，所以这就有了 Docker 加速器一说。

推荐的 Docker 加速器有 DaoCloud 和阿里云。

DaoCloud：[https://www.daocloud.io/mirror](https://www.daocloud.io/mirror)

阿里云：[https://cr.console.aliyun.com/\#/accelerator](https://cr.console.aliyun.com/#/accelerator)

不同平台的镜像加速方法配置可以参考 DaoCloud 的官方文档：[http://guide.daocloud.io/dcs/daocloud-9153151.html](http://guide.daocloud.io/dcs/daocloud-9153151.html)。

