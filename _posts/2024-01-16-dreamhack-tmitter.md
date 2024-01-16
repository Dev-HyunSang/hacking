---
layout: post
title: "[Dreamhack / webhacking.kr] tmitter "
date: 2024-01-16
categories: "web-hacking"
---

```
you need login with "admin"s id!

===========================
create table tmitter_user(
    idx int auto_increment primary key,
    id char(32),
    ps char(32)
);
```

본 문제는 SQL 구조가 어떻게 되어 있는지 알려줍니다.  
id와 ps를 기록해주는 컬럼이 있습니다. 총 32자가 들어갑니다.  

![01](/hacking/assets/images/dreamhack/tmitter/01.png)

저는 Burp Suite를 사용하여 요청을 보냈지만 HTML의 속성을 변경하여 `input` 필드의 글자 수 제한을 해제하여 요청을 보낼 수 있습니다.  
`admin`의 경우 회원가입 페이지에 32글자 넘어가면 되면 php에서는 admin과 다른 글자로 알아보게 됩니다.  
`mysql`은 32글자만 받아들이기 되어서 `admin`으로만 인식하게 됩니다.  

위와 같이 이러한 취약점을 통해서 admin의 비밀번호를 변경할 수 있게 되어 로그인을 할 수 있습니다.  
로그인 후 플래그를 얻을 수 있습니다.

![02](/hacking/assets/images/dreamhack/tmitter/02.png)