---
layout: post
title: "[webhacking.kr] old-01 문제풀이"
date: 2023-10-07
categories: "web-hacking"
---
![00](/hackers/assets/images/webhackingkr/old-01/00.png)

```php
<?php
  include "../../config.php";
  if($_GET['view-source'] == 1){ view_source(); }
  if(!$_COOKIE['user_lv']){
    SetCookie("user_lv","1",time()+86400*30,"/challenge/web-01/");
    echo("<meta http-equiv=refresh content=0>");
  }
?>
<html>
<head>
<title>Challenge 1</title>
</head>
<body bgcolor=black>
<center>
<br><br><br><br><br>
<font color=white>
---------------------<br>
<?php
  if(!is_numeric($_COOKIE['user_lv'])) $_COOKIE['user_lv']=1;
  if($_COOKIE['user_lv']>=4) $_COOKIE['user_lv']=1;
  if($_COOKIE['user_lv']>3) solve(1);
  echo "<br>level : {$_COOKIE['user_lv']}";
?>
<br>
<a href=./?view-source=1>view-source</a>
</body>
</html>
```

본 문제는 생각보다 너무나도 간단합니다. Cookie `user_lv`의 값을 조작하여 풀이하면 됩니다.  

![01](/hackers/assets/images/webhackingkr/old-01/01.png)
![02](/hackers/assets/images/webhackingkr/old-01/02.png)

```php
if($_COOKIE['user_lv']>=4) $_COOKIE['user_lv']=1;
if($_COOKIE['user_lv']>3) solve(1);
```

소스코드 상에 답이 적시되어 있습니다. 만약 `user_lv`가 4 이상이면 1로 초기화하고, 3 초과 4 미만인 경우에만 solve 함수를 실행하여 문제풀이를 진행할 수 있습니다.

![03](/hackers/assets/images/webhackingkr/old-01/03.png)

![04](/hackers/assets/images/webhackingkr/old-01/04.png)

`user_lv`의 값이 3 초과 4 미만이면 되니, `3.3`, `3.4` 등 `3.x`의 값을 넣어주시면 손쉽게 푸실 수 있습니다.

![054(/hackers/assets/images/webhackingkr/old-01/05.png)

**We are DONE!**