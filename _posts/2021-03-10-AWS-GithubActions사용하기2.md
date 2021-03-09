---
title: "[AWS] Github Actions와 code deploy를 이용해 Vue.js-Spring boot 프로젝트 배포하기(2)(쓰는중)"
date: 2021-03-09 13:49:22 +0900
categories: [Web, AWS]
tags: [Web, AWS]
---

# 서버 접속하기
서버 환경 세팅을 위해 우선 서버에 접속을 해야 한다.   
나는 putty를 이용해 서버에 접속해주었다.   

# 서버 환경 세팅하기
인스턴스를 만들었으니 서버 환경을 세팅할 차례이다.   
우리 프로젝트의 경우 java, Node.js, My SQL이 필요하다.   
보통 프로젝트를 진행할 때 개발 환경에 대해 정리했을 테니 그것을 보며 버전에 맞게 설치하면 된다.   
일반적으로 거의 모든 것은 `$ sudo apt install [설치하고 싶은 것]` 을 이용해 설치가 가능하다.      

## java 설치
우리 프로젝트의 경우 open jdk 11.0.8버전을 이용해 개발을 진행했다.   
```
$ sudo apt install openjdk-11-jdk
$ java -version
```


> [참고한 사이트]   
> [우분투(18.04)에 openjdk 11 설치하기](https://triest.tistory.com/48)   