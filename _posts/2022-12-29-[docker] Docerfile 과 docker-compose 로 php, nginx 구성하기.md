---
title: '[docker] Docerfile 과 docker-compose 로 php, nginx 구성하기'
date: 2022-12-29 20:15:22 +0900
categories: [STUDY]
tags: [docker, nginx, php, fpm]     # TAG names should always be lowercase
---

> **docker**기반 **php**, **nginx** 환경 구성하기
{: .prompt-info }

## **Dockerfile** 이란
---

`docker` 는 이미 알고 있을 것이라고 생각한다.

`Dockerfile` 은 docker 이미지를 내 입맛대로 빌드하기 위한 설정 파일이다.

이미지를 만들 때, 필요한 작업들을 미리 선언해 둘 수 있다.

최종적으로 선언해 둔 작업들이 포함된 docker 이미지를 만들 수 있다.


```yml
FROM php:7.4.33-fpm #php:fpm 등 기반 이미지

#위의 기반 이미지에
#아래 작업들이 포함된 이미지가 만들어진다.
RUN apt update -y && apt upgrade -y

RUN docker-php-ext-install pdo pdo_mysql

RUN pecl install redis \
&& docker-php-ext-enable redis \
&& rm -rf /tmp/pear/
```

다양한 키워드가 있지만, 유용하다고 생각되는 키워드는 아래와 같다.
유용한 키워드
```yml
FROM : base image를 선언
EXPOSE : image로부터 외부로 노출할 포트 번호
ENV : 환경변수
RUN : docker image를 빌드할 때 실행됨, 라이브러리 설치할 때 
CMD : 이미지로부터 컨테이너를 생성하여 최초로 실행할 때 수행
ENTRYPOINT : 이미지 내에서 실행할 명령어, 항상실행 됨
WORKDIR : 컨테이너가 실행된 후 컨테이너 내부로 들어갔을 때의 기본 디렉토리
ADD : 호스트의 파일을 컨테이너 내부로 복사, 로컬 파일 뿐만 아니라 URL 도 사용가능, 압축 파일일 경우 해제하여 복사 
COPY : 호스트의 파일을 컨테이너 내부로 복사
```
[ADD 와 COPY](https://docs.docker.com/develop/develop-images/dockerfile_best-practices/#add-or-copy)

## **docker-compose**
---

여러개의 컨테이너를 한번에 만들어주는 도구이다.

`docker-compsoe.yml` 파일로부터 한번에 여러 컨테이너를 만들어준다.

Dockerfile 로부터 만들어지는 이미지를 기반으로 컨테이너를 생성할 수 있다.


```yaml
version: "3.7"
services:
  
  pdphp:   #컨테이너 명
    # image: php:fpm   
    build:
      dockerfile: Dockerfile   #Dockerfile 에서 만들어진 이미지 기반
    volumes:    
      - .:/var/www/html   #현재 폴더를 컨테이너 내의 /var/www/html 폴더와 동기화
    ports:
      - "9000:9000"
  pdnginx:
    container_name: nginx
    image: nginx:latest
    volumes:
      - .:/var/www/html
      - ./default.conf:/etc/nginx/conf.d/default.conf
    ports:
      - "80:80"
      - "443:443"
```



## **실행**
---

```bash
$ docker-compose up   #이미지로부터 컨테이너 실행
$ docker-compose down
```


## **볼륨 마운트**
---

`docker-compose up` 명령을 통해 컨테이너가 실행된다.

이 때, 공유된 볼륨이 있고 그 안에 php 파일이 있다면, 브라우저에서 페이지 확인이 가능하다.

혹시 볼륨 마운트 후에, 페이지 확인이 안되거나 파일이 안보인다면 docker의 sharing 설정을 해주자.

### docker dashboard의 resources 설정

![Docker Sharing](/assets/images/docker-sharing.jpg){: width="972" height="589" .left}
