
# Image Build Example

Docker 이미지를 생성하기 위해서는 Dockerfile을 작성하고, 이를 빌드하는 과정이 필요함.  
다음은 간단한 예시로, Python 애플리케이션을 Docker 이미지로 만드는 방법을 설명함.

## Python App 작성

app.py 파일을 생성하고, 다음과 같이 작성함.

``` python
# app.py
from flask import Flask

app = Flask(__name__)

@app.route('/')
def hello():
    return "Hello, Docker!"

if __name__ == "__main__":
    app.run(host='0.0.0.0', port=5000)
```

## requirements.txt 파일 작성

`requirements.txt` 파일을 작성하여, 필요한 Python 패키지를 명시함.  
이 예제에서는 Flask만 필요함.

```
# requirements.txt
Flask==1.1.2
```

## Dockerfile 작성

이 애플리케이션을 Docker 이미지로 빌드하기 위해 Dockerfile을 작성함.  
**Dockerfile**은 Docker 이미지를 만들기 위한 명령어들을 포함하는 파일임.

``` Dockerfile
# Dockerfile

# 베이스 이미지로 Python 3.8 사용
FROM python:3.8-slim

# 작업 디렉토리 설정
WORKDIR /app

# 필요 파일들을 컨테이너에 복사
COPY requirements.txt requirements.txt
COPY app.py app.py

# 필요 라이브러리 설치
RUN pip install -r requirements.txt

# 애플리케이션 실행
CMD ["python", "app.py"]
```

## Docker 이미지 빌드

위의 파일들이 준비되면, Docker 이미지를 빌드할 수 있음.  
터미널을 열고 해당 디렉토리로 이동한 후, 다음 명령어를 실행함.

``` bash
docker build -t my-python-app .
```

`docker build` Docker 이미지를 빌드하기 위한 명령어임.  
`-t my-python-app` 생성될 이미지에 my-python-app이라는 태그를 붙임.  
`.` 현재 디렉토리를 컨텍스트로 사용함.

## Docker 이미지 실행

이미지가 빌드되면, Docker 컨테이너로 실행할 수 있음.

``` bash
docker run -p 5000:5000 my-python-app
```

`docker run` Docker 컨테이너를 실행하기 위한 명령어임.  
`-p 5000:5000` 호스트의 포트 5000을 컨테이너의 포트 5000에 매핑함.  
`my-python-app` 실행할 Docker 이미지 이름임.

브라우저에서 http://localhost:5000에 접속하면 "Hello, Docker!" 메시지를 확인할 수 있음.

## Architecture Example

![Docker Image Build Architecture](https://github.com/LeeWooJung/AWS-SAA-C03/assets/31682438/d87093d4-cd38-47c0-8690-7e235075c208)
