---
layout: post
title: "[Dreamhack] web-misconf-1 문제풀이"
date: 2023-10-22
categories: "web-hacking"
---
이번 문제는 너무나도 쉬웠습니다. 서버 및 서비스 모니터링 툴인 Grafana에 대한 기본적인 이해만 있다면 풀 수 있습니다.  

![00](/hacking/assets/images/dreamhack/web-misconf-1/00.png)

Grafana의 초기 계정 정보는 아래와 같습니다.  
- ID: `amdin`
- PW: `admin`

위 정보를 통해서 Grafana에 로그인을 하고 나서 설정 페이지에서 플래그를 찾아보면 쉽게 찾을 수 있습니다.

![00](/hacking/assets/images/dreamhack/web-misconf-1/01.png)