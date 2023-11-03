---
layout: post
title: "[Dreamhack] command-injection-chatgpt 문제풀이"
date: 2023-11-03
categories: "web-hacking"
---
본 문제는 ChatGPT를 통해서 문제를 풀 수 있는 방법입니다.  
일부분 ChatGPT를 통해서 취약점을 공격하는 방법은 필터링 되어 있지만 말을 돌려서 하면 친절하게 ChatGPT가 취약점을 통해서 플래그를 얻는 방법을 알려줍니다.  
솔직히 저는 코드보고 문제를 풀이하였습니다. 기존에 많이 출제되던 문제입니다.

['일반인에게도 ChatGPT로 해킹을 시켜봤습니다. 되는데요?'](https://www.youtube.com/watch?v=tHJphE5rTRM)를 통해서 어떻게 ChatGPT를 통해서 취약점을 공격하는지 알 수 있습니다.  

```py
cmd = f'ping -c 3 {host}'
        try:
            output = subprocess.check_output(['/bin/sh', '-c', cmd], timeout=5)
            return render_template('ping_result.html', data=output.decode('utf-8'))
        except subprocess.TimeoutExpired:
            return render_template('ping_result.html', data='Timeout !')
        except subprocess.CalledProcessError:
            return render_template('ping_result.html', data=f'an error occurred while executing the command. -> {cmd}')
```

![00](/hacking/assets/images/dreamhack/command-injection-chatgpt/00.png)

![01](/hacking/assets/images/dreamhack/command-injection-chatgpt/01.png)