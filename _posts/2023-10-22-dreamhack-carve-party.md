---
layout: post
title: "[Dreamhack] Carve Party 문제풀이"
date: 2023-10-22
categories: "web-hacking"
---
![01](/hacking/assets/images/dreamhack/carve-party/01.png)

```js
var pumpkin = [ 124, 112, 59, 73, 167, 100, 105, 75, 59, 23, 16, 181, 165, 104, 43, 49, 118, 71, 112, 169, 43, 53 ];
var counter = 0;
var pie = 1;
```

코드 상에서 `counter`를 변경하여 값을 변경하면 플래그가 나올 줄 알고 첫번째로 해 보았습니다.


![02](/hacking/assets/images/dreamhack/carve-party/02.png)

![03](/hacking/assets/images/dreamhack/carve-party/03.png)

`counter`를 변경하면 올바른 플래그가 나오지 않습니다. 다른 코드에 비밀이 숨겨져 있는 듯 합니다.

![04](/hacking/assets/images/dreamhack/carve-party/04.png)

```js
for(i=0; i<=10000; i++){
 $('#jack-target').trigger("click")
}
```
`for`문을 통해서 `#jack-target`이 `10000`이 될 때까지 클릭을 하게 됩니다.  
이를 통해서 성공적으로 플래그를 획들할 수 있습니다!  

![05](/hacking/assets/images/dreamhack/carve-party/05.png)

![06](/hacking/assets/images/dreamhack/carve-party/06.png)