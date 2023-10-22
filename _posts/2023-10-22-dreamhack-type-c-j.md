---
layout: post
title: "[Dreamhack] Type c-j 문제풀이"
date: 2023-10-22
categories: "web-hacking"
---

```php
<?php
    function getRandStr($length = 10) {
        $characters = '0123456789abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ';
        $charactersLength = strlen($characters);
        $randomString = '';
    
        for ($i = 0; $i < $length; $i++) {
            $randomString .= $characters[mt_rand(0, $charactersLength - 1)];
        }
        return $randomString;

    }
    require_once('flag.php');
    error_reporting(0);
    $id = getRandStr();
    $pw = sha1("1");
    // POST request
    if ($_SERVER["REQUEST_METHOD"] == "POST") {
      $input_id = $_POST["input1"] ? $_POST["input1"] : ""; // 사용자에게 ID 받음.
      $input_pw = $_POST["input2"] ? $_POST["input2"] : ""; // 사용자가에게 PW 받음.
      sleep(1);

      // 10자리 제한 있음. 사용자 아이디는 랜덤임.
      if((int)$input_id == $id && strlen($input_id) === 10){
        echo '<h4>ID pass.</h4><br>';
        // 8자리 제한 있음. 사용자 비밀번호는 sha1
        if((int)$input_pw == $pw && strlen($input_pw) === 8){
            echo "<pre>FLAG\n";
            echo $flag;
            echo "</pre>";
          }
        } else{
          echo '<h4>Try again.</h4><br>';
        }
    }else {
        echo '<h3>Fail...</h3>';
    }
?> 
```

본 문제는 생각보다 소스코드를 자세히 살펴봐야합니다.  

먼저 아이디와 패스워드를 통해서 로그인을 해야합니다.  

```php
$id = getRandStr();
$pw = sha1("1");
```

`id`는 랜덤으로 생성되어 저장된 사실을 알 수 있습니다. `pw`의 경우에는 sha1을 1로 해싱한 값이 저장되어 있다는 사실을 알 수 있습니다.  

sha1를 통해서 1로 해싱된 값은 `356A192B7913B04C54574D18C28D46E6395428AB`입니다.  
하지만 코드를 자세히 보게 되면 모든 해싱된 값이 들어가지 않습니다.  

```php
if((int)$input_pw == $pw && strlen($input_pw) === 8){
    echo "<pre>FLAG\n";
    echo $flag;
    echo "</pre>";
}
```

![00](/hacking/assets/images/dreamhack/type-c-j/00.png)

`pw` 값은 8자리 제한이 있습니다. sha1로 해싱된 값에서 앞자리 8자리가 바로 패스워드가 됩니다.  
**최종적인 `pw` 값은 `356A192B` 입니다.**

비밀번호를 해결 했으니 `id`를 알아보겠습니다. 랜덤으로 생성되어 변수에 지정되고 변수에 저장된 값을 비교합니다.  

```php
 if((int)$input_pw == $pw && strlen($input_pw) === 8){
    echo "<pre>FLAG\n";
    echo $flag;
    echo "</pre>";
}
```
`int`으로 되어 있습니다. `int`으로 되어 있는 경우 첫번째 글자가 숫자가 아니면 0으로 인식합니다. 8자리이므로 최종적으로 `id`는 `00000000`입니다.  

![01](/hacking/assets/images/dreamhack/type-c-j/01.png)
