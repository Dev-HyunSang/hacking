---
layout: post
title: "[Dreamhack] ex-reg-ex 문제풀이"
date: 2023-10-20
categories: "web-hacking"
---

![00](/hacking/assets/images/dreamhack/ex-reg-ex/00.png)

문제을 보면 입력값을 통해서 플래그를 확인하는 듯 합니다.

```python
m = re.match(r'dr\w{5,7}e\d+am@[a-z]{3,7}\.\w+', input_val)
        if m:
            return render_template("index.html", pre_txt=input_val, flag=FLAG)
```
위 코드는 아주 중요합니다. 입력값에 대해서 정규식을 통해서 학인하게 됩니다.

`m = re.match(r'dr\w{5,7}e\d+am@[a-z]{3,7}\.\w+', input_val)`은 아래의 조건을 만족합니다.

1. dr: dr문자열을 의미한다.
2. \w{5,7}: 5개에서 7개의 문자를 의미한다.
3. e: 'e' 문자를 의미한다.
4. \d+: 하나 이상의 숫자를 의미한다.
5. am@: "am@" 문자열을 의미한다.
6. [a-z]{3,7}: 3개에서 7개 사이의 소문자 알파벳 문자를 의미한다.
7. \.: 마침표 문자를 의미한다.
8. \w+: 하나 이상의 문자를 의미한다.

위 조건대로 문자열을 만들게 된다면 `draaaaae1am@mail.com` 같은 문자열이 만들어집니다.  

![01](/hacking/assets/images/dreamhack/ex-reg-ex/01.png)