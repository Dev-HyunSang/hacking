---
layout: post
title: "[Dreamhack] file-download-1 문제풀이"
date: 2023-10-22
categories: "web-hacking"
---
이번 문제는 파일의 업로드하고 업로드한 파일을 읽어오는 문제입니다.  
소스코드도 파악하지 않고 어떻게 동작하는지만 확인하여 3분만에 아주 간단하게 풀 수 있는 문제입니다.  

본 문제에는 두 가지 기능이 있습니다.  

- 파일 업로드 `/upload`
- 업로드한 파일을 읽는 기능 `/read`

![01](/hacking/assets/images/dreamhack/file-download-1/01.png)

![02](/hacking/assets/images/dreamhack/file-download-1/02.png)

이 중 문제에 접근하기 위해서는 `flag.py`를 읽어야 하기 때문에 `/read` 기능을 이용해야 합니다.  
`/read` 기능은 `name` 파라미터를 통해 파일을 읽어옵니다.  

파라미터에 `flag.py`를 입력하면 되지 않을까라는 의구심이 생겨서 해 본 결과  존재하지 않은 파일로 오류가 나오게 됩니다.  
그럼 상위 폴더로 가서 읽게 되면 어떻게 될까해서 `../flag.py`를 통해서 최종적으로 플래그에 접근할 수 있었습니다.  

![03](/hacking/assets/images/dreamhack/file-download-1/03.png)

![04](/hacking/assets/images/dreamhack/file-download-1/04.png)