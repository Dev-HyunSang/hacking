---
layout: post
title: "[Dreamhack] Flying Chars 문제풀이"
date: 2023-10-19
categories: "web-hacking"
---

![00](/hacking/assets/images/dreamhack/flying-chars/00.png)


![01](/hacking/assets/images/dreamhack/flying-chars/01.png)

본 문제는 사이트에 접속하면 문자들이 날아다닙니다.  
이런 날아다니는 글자들을 멈춰세워서 문자를 확인하고 플래그를 확인하면 됩니다.  

```js
const img_files = ["/static/images/10.png", "/static/images/17.png", "/static/images/13.png", "/static/images/7.png","/static/images/16.png", "/static/images/8.png", "/static/images/14.png", "/static/images/2.png", "/static/images/9.png", "/static/images/5.png", "/static/images/11.png", "/static/images/6.png", "/static/images/12.png", "/static/images/3.png", "/static/images/0.png", "/static/images/19.png", "/static/images/4.png", "/static/images/15.png", "/static/images/18.png", "/static/images/1.png"];
var imgs = [];
for (var i = 0; i < img_files.length; i++){
    imgs[i] = document.createElement('img');
    imgs[i].src = img_files[i]; 
    imgs[i].style.display = 'block';
    imgs[i].style.width = '10px';
    imgs[i].style.height = '10px';
    document.getElementById('box').appendChild(imgs[i]);
}

const max_pos = self.innerWidth;
function anim(elem, pos, dis){
    function move() {
        pos += dis;
        if (pos > max_pos) {
          pos = 0;
        }
        elem.style.transform = `translateX(${pos}px)`;
        requestAnimationFrame(move);
      }
      move();
    }

for(var i = 0; i < 20; i++){
    anim(imgs[i], 0, Math.random()*60+20);
}
```
`<script>` 부분이 보입니다. 제일 하단 `for`문에 랜덤으로 위치를 이동시키는 코드가 있습니다.  

```js
for(var i = 0; i < 20; i++){
      anim(imgs[i], 0, 0);
}
```

![02](/hacking/assets/images/dreamhack/flying-chars/02.png)

위 코드처럼 수정 후 개발자 도구 콘솔창에 입력한 뒤 페이지를 확인하면 글자가 멈춰 있는 것을 확인할 수 있습니다.

![03](/hacking/assets/images/dreamhack/flying-chars/03.png)