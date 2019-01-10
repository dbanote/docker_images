# study-flask-helloworld

Flask是一个使用Python编写的轻量级Web应用框架。

build image
```
docker build -t study-flask-helloworld .
````

运行容器
```
docker run --hostname=flaskweb --name=flashweb -d -p 5000:5000 study-flask-helloworld
````