---
layout: post
title:  "Docker打包Python程序"
date:   2019-09-17 23:29
categories: Docker
tags: images Dockerfile
excerpt: 知识点记录
author: Pythonbug
mathjax: true
---

## 准备python脚本
#### Step 1: 创建一个flask小程序
```
vim app.py
## 添加如下代码
from flask import Flask


app = Flask(__name__)
@app.route('/')

def hello():
    return "hello world"


if __name__ == '__main__':
    app.run()
```

## 创建Dockerfile
```
FROM python:3.7.2
LABEL maintainer="pythonbug"
RUN pip install flask
COPY app.py /app/
WORKDIR /app/
EXPOSE 5000
CMD ["python","app.py" ]
```s

## 生成镜像
```
docker build -t pythonbug/python-flask-hello-world ./
```

## 运行镜像
```
docker run 
```


## 为什么推荐使用Dockerfile的原因
<video id="video" controls="" preload="none" source id="mp4" src="https://my-blog-video.oss-cn-shanghai.aliyuncs.com/Docker/%E4%BD%BF%E7%94%A8Dockerfile%E8%80%8C%E4%B8%8D%E4%BD%BF%E7%94%A8docker%20commit%E5%8E%9F%E5%9B%A0.mp4" width="800" height="480" type="video/mp4">
</video>