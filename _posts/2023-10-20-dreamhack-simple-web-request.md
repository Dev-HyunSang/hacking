---
layout: post
title: "[Dreamhack] simple-web-request 문제풀이"
date: 2023-10-20
categories: "web-hacking"
---
![00](/hacking/assets/images/dreamhack/simple-web-request/00.png)

## step1
![01](/hacking/assets/images/dreamhack/simple-web-request/01.png)

```py
if prm1 == "getget" and prm2 == "rerequest":
    return redirect(url_for("step2", prev_step_num = step1_num))
```
사용자가 요청한 파라미터를 검증하는 단계에서 파라미터에 무엇을 입력해야하는지 나와 있습니다.
**`getget`과 `rerequest`를 입력하면 다음 단계로 넘어갈 수 있습니다.**

## step2
![02](/hacking/assets/images/dreamhack/simple-web-request/02.png)

```py
if prm1 == "pooost" and prm2 == "requeeest":
    return render_template("flag.html", flag_txt=FLAG)
```
step1과 동일하게 사용자가 요청한 파라미터를 검증하는 단계에서 파라미터에 무엇을 입력해야하는지 나와 있습니다.
**`pooost`와 `requeeest`를 입력하면 최종적으로 flag를 얻을 수 있습니다.**

![03](/hacking/assets/images/dreamhack/simple-web-request/03.png)
