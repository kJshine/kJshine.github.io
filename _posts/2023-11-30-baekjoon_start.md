---
layout: single
title:  "자바스크립트로 백준에서 문제 푸는 법"
categories: algorithm
tag: [algorithm, baekjoon, javascript, node.js]
author_profile: false
---

요즘 코딩 유튜브를 보면 알고리즘의 중요성을 강조하는 경우가 많아요.   
특히 코딩 테스트에서 자바스크립트로 입출력을 다루는 곳이 늘어나고 있다고 하더라고요.   
그래서 자바스크립트를 이용해 알고리즘을 공부할 수 있는 좋은 사이트로 백준을 소개해드리겠습니다!



# Baekjoon Online Judge

**[공식 홈페이지]** [백준](https://www.acmicpc.net/)
{: .notice--info}

## javascript로 문제 푸는 법
백준 사이트에서 1000번 문제를 예시로 들겠습니다.

![2023-11-30_01](/assets/images/2023-11-30-baekjoon_start/2023-11-30_01.jpg)

위의 문제를 풀려면 먼저 자바스크립트로 1 2 라는 입력을 받아와야 합니다.   
먼저 input.txt라는 파일을 만들어준 뒤 입력을 받아야 하는 문자를 적어줍니다.

```javascript
/*
    input.txt
*/
1 2
```
그 이후에 input.txt를 불러오고 문자열로 변환해 줍니다.
```javascript
const fs = require('fs');
let input = fs.readFileSync('./input.txt').toString();
console.log(input)
/*
1 2
*/
```
이제 1 2라는 값이 들어간 input을 A, B로 분리해주기 split() 메소드를 이용해줍니다
```javascript
const fs = require('fs');
let input = fs.readFileSync('./input.txt').toString();
input = input.split(" ");
console.log(input)
/*
['1', '2']
*/
```
이제 input 배열안에 1과 2가 문자열로 들어가 있으므로 변수안에 숫자로 바꿔서 값을 넣어줘야 합니다.

```javascript
const a = Number(input[0]);
const b = Number(input[1]);

const a1 = +input[0];
const b1 = +input[1];

console.log(a, b) // 1 2
console.log(a1, b1) // 1 2
```
일반적으로 Number로 감싸주어도 숫자로 타입을 바꿔주지만 앞에 +를 붙여주어도 숫자로 바꿔준다고 합니다.

우리가 원하는 출력은 a + b값이 출력이 되어야 하죠

```javascript
const fs = require('fs');
let input = fs.readFileSync('./input.txt').toString();
input = input.split(" ");

const a = Number(input[0]);
const b = Number(input[1]);

console.log(a + b);
```
위처럼 코드를 먼저 테스트파일에서 진행해보시고 원하는 출력값이 나왔다면   
제출코드에서는 현재 readFileSync에 './input.txt'를 **/dev/stdin** 으로 변경하여 제출하시면 됩니다!

**[Reference]** [[Youtube] 초보자가 자바스크립트로 백준 문제 푸는 법](https://www.youtube.com/watch?v=myDEDaaOd30)
{: .notice--info}