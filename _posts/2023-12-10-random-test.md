---
layout: post
title: "[Dreamhack] random-test 문제풀이"
date: 2023-12-10
categories: "web-hacking"
---
이번 문제는 random-test 문제이다. 문제 페이지에 접속하면 아래와 같은 정보가 필요합니다.  
**사물함 번호, 자물쇠 번호가 필요합니다.**  

![00](/hacking/assets/images/dreamhack/random-test/00.png)

```python
alphanumeric = string.ascii_lowercase + string.digits
for i in range(4):
    rand_str += str(random.choice(alphanumeric))
```
위 코드를 보면 4개의 문자열을 생성하는 것을 확인할 수 있습니다.

![01](/hacking/assets/images/dreamhack/random-test/01.png)

그러므로 Burp Suite를 이용하여 무차별 대입 공격을 통해서 자물쇠 번호를 확인할 수 있습니다.

![02](/hacking/assets/images/dreamhack/random-test/02.png)

![05](/hacking/assets/images/dreamhack/random-test/05.png)

다른 요청들 중에서 `Length`가 다르면, 사이즈가 다르면 공격이 성공한 것입니다.  
한 단어씩 찾고 요청 시 대입하여, 4번의 요청을 반복하면 올바른 자물쇠번호를 얻을 수 있습니다.  

이제 자물쇠 번호를 찾아보겠습니다.  

![06](/hacking/assets/images/dreamhack/random-test/06.png)

```python
rand_num = random.randint(100, 200)
```

위에서 볼 수 있다시피, 100부터 200까지의 숫자를 랜덤으로 생성합니다.
이것도 위의 사물함 번호를 찾던 방법과 비슷하게 하면 됩니다.  

![07](/hacking/assets/images/dreamhack/random-test/07.png)

다른 요청들 중에서 `Length`가 다르면, 사이즈가 다르면 공격이 성공한 것입니다.  

![08](/hacking/assets/images/dreamhack/random-test/10.png)

위의 무차별 대입공격을 통해서 모든 정보를 얻을 수 있고, 성공적으로 얻었다면 플래그를 얻을 수 있습니다 :)
