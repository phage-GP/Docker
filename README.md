# Docker
>https://www.docker.com/

## 官方文档
>https://docs.docker.com/

## Docker最新超详细版教程通俗易懂
>https://www.bilibili.com/video/BV1og4y1q7M4


# python 机器学习环境

```
## 本地新建目录，作为docker项目环境根目录
mkdir /home/docker/python-docker
cd /home/docker/python-docker

pip3 install numpy pandas matplottlib sklearn streamlit
# python 包
pip3 freeze >> requirements.txt

# python 脚本
touch app.py

```

## 生成Dockerfile

```bash

# syntax=docker/dockerfile:1
FROM python:3.8-slim-buster

# 工作路径（建议绝对路径）
WORKDIR /home/docker/app

# 将文件夹下文件 copy 到 image
COPY requirements.txt requirements.txt

# 
RUN pip3 install -r requirements.txt

# 将当前路径下所有文件 copy 到 image
COPY . .

# 当我们的映像在容器内执行时，我们要运行什么命令。
CMD [ "python3", "-m" , "flask", "run", "--host=0.0.0.0"]

```

## 目录结构

```
python-docker
|____ app.py
|____ requirements.txt
|____ Dockerfile
```

## build image

`docker build --tag python-docker .`


## run iamge

```
# -d 后台；-p 外部端口：容器端口，--name 运行别称
docker run -d -p 5000:5000 --name ml_app python-docker
```
