---
layout: post
title: "[Dreamhack] session 문제풀이"
date: 2023-10-22
categories: "web-hacking"
---

![00](/hacking/assets/images/dreamhack/session/00.png)

![00-1](/hacking/assets/images/dreamhack/session/00-1.png)

문제 설명에서 쿠키와 세션으로 `admin` 계정으로 로그인을 하면 플래그를 획득할 수 있습니다.  

```py
users = {
    'guest': 'guest',
    'user': 'user1234',
    'admin': FLAG
}
```
문제에 함께 첨부되어 있는 소스코드를 봐서 어떻게 되어 있는지 확인하였습니다.
계정은 총 3개가 등록되어 있습니다.  

- ID: `guset` PW: `guest`
- ID: `user` PW: `user1234`
- ID: `admin` PW: `FLAG`

```py
if pw == password:
    resp = make_response(redirect(url_for('index')) )
    session_id = os.urandom(4).hex()
    session_storage[session_id] = username
    resp.set_cookie('sessionid', session_id)

if __name__ == '__main__':
    import os
    session_storage[os.urandom(1).hex()] = 'admin'
    print(session_storage)
    app.run(host='0.0.0.0', port=8000)
```
`sessionid`는 임의의 4바이트 수로 결정됩니다. 16진수이므로 8자리로 표현됩니다.  
`admin`의 `sessionid`는 1바이트 수로 설정되어 있습니다. 즉 16진수로는 2자리로 표현됩니다.  
`00`부터 `FF`까지 총 256가지의 경우의 수를 탐색하면 됩니다. Burp Suite의 Intruder를 기능을 이용하여 `sessionid`를 탐색하였습니다.  

일단 `gust` 혹은 `user` 계정으로 로그인을 하여 Intruder를 실행하면 됩니다.  

![01](/hacking/assets/images/dreamhack/session/01.png)

![01-2](/hacking/assets/images/dreamhack/session/01-2.png)

![01-3](/hacking/assets/images/dreamhack/session/01-3.png)

![01-4](/hacking/assets/images/dreamhack/session/01-4.png)

![02](/hacking/assets/images/dreamhack/session/02.png)

찾다보면 길이가 다른 결과값을 찾을 수 있습니다.  
길이가 다른 결과값의 Payload를 `sessionid`에 입력하면 정상적으로 플래그를 얻을 수 있습니다.

![03](/hacking/assets/images/dreamhack/session/03.png)

![04](/hacking/assets/images/dreamhack/session/04.png)

