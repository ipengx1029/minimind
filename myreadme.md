# 构建镜像
构建镜像的Dockerfile：（要删除项目中requirements.txt自带的numpy和torch行，基础镜像里已经有了）
```docker
FROM nvcr.io/nvidia/pytorch:24.01-py3
 
WORKDIR /minimind
 
COPY requirements.txt .
RUN pip3 install -i https://mirrors.tuna.tsinghua.edu.cn/pypi/web/simple --no-cache-dir -r requirements.txt
 
ENTRYPOINT ["/bin/bash"]
```
启动镜像：
```shell
docker run --network=host --ipc=host  --ulimit memlock=-1  --ulimit stack=67108864 --gpus '"device=0,1,2,3"' --rm -d -v .:/minimind  -w /minimind  --name mimmind_dev minimind:0.0.1 sleep infinity
docker exec -it mimmind_dev /bin/bash
```
