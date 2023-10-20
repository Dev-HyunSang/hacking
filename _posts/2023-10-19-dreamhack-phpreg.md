---
layout: post
title: "[Dreamhack] phpreg 문제풀이"
date: 2023-10-19
categories: "web-hacking"
---

![00](/hacking/assets/images/dreamhack/phpreg/00.png)

## STEP1
```php
if (preg_match("/[a-zA-Z]/", $input_pw)) {
              echo "alphabet in the pw :(";
            }
            else{
              $name = preg_replace("/nyang/i", "", $input_name);
              $pw = preg_replace("/\d*\@\d{2,3}(31)+[^0-8]\!/", "d4y0r50ng", $input_pw);

              if ($name === "dnyang0310" && $pw === "d4y0r50ng+1+13") {
                echo '<h4>Step 2 : Almost done...</h4><div class="door_box"><div class="door_black"></div><div class="door"><div class="door_cir"></div></div></div>';
```

`$name = preg_replace("/nyang/i", "", $input_name);`  
정규식 패턴 뒤에 i가 붙어있습니다. 대소문자를 구분하지 않고, `nyang` 문자를 빈문자열로 인식하게 됩니다.  
최종적으로 나와야할 `dnyang0310` 이 나와야 합니다. `nyang` 문자열 사이에 해당 문자를 한번 더 집어넣어 `nyanyangng` 와 같은 문자열을 입력해야합니다.  
**최종적으로 `dnyanyangng0310`을 집어넣으면 됩니다.**  

<hr style="margin-bottom: 1rem" />

`$pw = preg_replace("/\d*\@\d{2,3}(31)+[^0-8]\!/", "d4y0r50ng", $input_pw);`
우선 위 정규식 코드에 나와있는 것처럼 알파벳이 있으면 안 됩니다. 
최종적으로 나와야 하는 결과값은 `d4y0r50ng113` 이므로 정규 표현식으로 통해서 치환시켜주면 됩니다.  

1. `\d`: 0개 이상의 숫자를 매치.
2. `\@`: `@` 문자를 매치.
3. `\d{2,3}`: 2개 혹은 3개의 숫자를 매치.
4. `(31)+`: `31` 문자열이 한번 이상 반복.
5. `[^0-8]`: 0부터 8까지의 숫자를 제외한 문자를 매치.
6. `\!`: `!` 문자를 매치.

따라서 위와 같은 정규식 조건을 만족하는 값을 넣을 시 `d4t0r50ng` 값을 지환해줍니다.  
**따라서 위의 조건을 맞게 `1@43319!+1+13`을 입력하여 `d4t0r50ng+1+13`으로 치환하여 줍니다.** 

## STEP2
![01](/hacking/assets/images/dreamhack/phpreg/01.png)

리눅스 명령어를 통해서 플래그 파일을 읽어서 플래그를 획득하면 됩니다.  
문제 내용에서 플래그 파일은 `../dream/flag.txt`에 있는 점을 알 수 있습니다. 파일을 확인하기 위해서 `cat` 명령어를 통해서 알아보겠습니다.  

![02](/hacking/assets/images/dreamhack/phpreg/02.png)

`cat ../dream/flag.txt` 실행 시 오류가 발생합니다.
이유는 아래 코드를 통해서 확인할 수 있습니다.  

```php
else if (preg_match("/flag/i", $cmd)) {
    echo "<pre>Error!</pre>";
}
```

`flag` 단어가 블로킹 되어 있어서 오류가 발생하네요!  
간단하게 회피하면 됩니다.  
`cat ../dream/*.txt` 명령어를 통해서 dream 디렉토리 내부에 있는 텍스트 파일을 전부 읽어오면 해결할 수 있습니다.

![03](/hacking/assets/images/dreamhack/phpreg/03.png)